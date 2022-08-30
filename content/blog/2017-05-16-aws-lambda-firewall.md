---
title: Knock first firewall for AWS Security Groups
date: 2017-05-16 22:21:53
type: posts
tags:
 - AWS
 - AWS lambda
 - AWS API Gateway
---
I recently [setup a Bastion host](./2017-05-01-setting-up-bastion-host-aws.html) to secure a development environment on AWS. The Bastion only exposes port 22 for SSH and I wanted to restrict access to a whitelist of authorized IP addresses rather than leave port 22 open to the internet. Further - I wanted to restrict 443 and 80 inbound to the development environment so that only authorized users/developers could access the pre-release builds deployed there.

But I and others on my team switch IP addresses often and don't want to hassle with manual manipulation of AWS Security Groups each time I move networks in meatspace. So I threw together [a "knock for access" firewall using API Gateway & lambda](https://github.com/ets/aws-lambda-firewall) to conveniently add and expire authorized IP addresses on the applicable Security Groups. Enjoy!
