---
title: Setting up a Bastion host on AWS
date: 2017-05-18
type: posts
tags:
 - AWS
 - bastion
 - jumphost

---
When setting up my latest development environment at AWS, I wanted to deploy all EC2 services on a private VPC and simply route all traffic to them through a Bastion host (aka jump host). AWS maintains a an [excellent CloudFormation quickstart guide & template here](http://docs.aws.amazon.com/quickstart/latest/linux-bastion/welcome.html) and it's what I used to get started. After completing that guide I put a new entry for the Bastion host in my ssh config like so:
```
Host bastion
  Hostname ec2-XX-XXX-XXX-XXX.compute-1.amazonaws.com
  User ec2-user
  IdentityFile ~/path/to/your/ssh-key.pem
  AddKeysToAgent yes
  UseKeychain yes
```

Those last two lines are optional - but I like to [leverage the Keychain on my MacBookPro](http://www.openssh.com/txt/release-7.2) for storing keys and their respective passphrases. Accepting the host key into your known_hosts file can avoid some pain going forward, so I recommend connecting directly to the bastion before continuing.

To test my setup, I launched a EC2 instance in my private VPC and configured it in my ssh config like so:
```
Host 10.100.*.*
  ProxyCommand ssh ec2-user@bastion -W %h:%p
  User ec2-user
  IdentityFile ~/path/to/your/ssh-key.pem
  AddKeysToAgent yes
  UseKeychain yes
```

The magic happens on the second line with the ProxyCommand instructing SSH to jump through Bastion to route to any of the private IP addresses used in my development environment VPC. Unfortunately, my first attempt to connect failed. I poked around in the Bastion's SSHD config and realized that the CloudFront template was so hardened that it wasn't going to support the transparent sessions I wanted. I needed to modify /etc/ssh/sshd_config and add the following just below the PAM section:
```
PermitOpen any
AllowTCPForwarding yes
```
After making the change be certain to restart the sshd service on Bastion.

Part of the beauty of the CloudFormation design is that it uses an AutoScaling group to automatically tear down unresponsive Bastions and spin up replacements - even adapting to availability zone issues. When that happens the replacement Bastion will be configured with template defaults, so to ensure my sshd_config change would survive a failover, I copied the LaunchConfig and edited the user data to include the following:
```
perl -pi -0 -w -e 's/UsePAM yes/UsePam yes\n\n# Added by ets to support transparent pass through\nPermitOpen any\nAllowTCPForwarding yes/' sshd_config
```
Then I replaced the currently configured LaunchConfig on my AutoScaling group with my copy.

Now simply asking SSH to connect to my new services in the private VPC worked transparently!
To make session more efficient using this type of proxy, I added the following to my Bastion host entry in ssh config:
```
ControlPath ~/.ssh/cm-%r@%h:%p
ControlMaster auto
ControlPersist 10m
```

If you're an [ansible](https://www.ansible.com/) fan like me, you can take advantage of that same technique with a change to ansible.cfg:
```
ssh_args = -o ControlMaster=auto -o ControlPersist=30m
control_path = ~/.ssh/ansible-%%r@%%h:%%p
```

If you're curious how to further protect your Bastion host with a whitelist for port 22 while also supporting users who are behind dynamic IPs then you'll want to [check out my aws-lambda-firewall project](/2017/05/16/2017-05-16-aws-lambda-firewall/).
