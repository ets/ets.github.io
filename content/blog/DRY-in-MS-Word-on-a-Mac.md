---
title: DRY in MS Word on a Mac
date: 2018-11-09
type: posts
tags:
---

Lucky me had the opportunity to review & adopt 60+ HITRUST policies for [HealthPrize](https://www.healthprize.com) this week. My friendly outside council delivered the policies as individual MS Word documents. So to make the process of inserting our logo, stamping the adoption date, and generally modifying the boilerplate to fit our needs I decided to apply a little macro magic. YMMV:
```
Sub HPTPolicies()
'
' HPTPolicies Macro
'
'
    With Selection
    .HomeKey Unit:=wdStory
        With .Find
        .ClearFormatting
        .Text = "[[INSERT LOGO]]"
        Do While .Execute
            Selection.MoveRight
            Selection.InlineShapes.AddPicture fileName:="/Volumes/mydrive/afolder/HPTlogo.png", LinkToFile:=False, SaveWithDocument:=True
        Loop
        End With
    End With
    With Selection
    .HomeKey Unit:=wdStory
    With .Find
        .ClearFormatting
        .Text = "[[INSERT LOGO]]"
        Do While .Execute
            Selection.Delete
        Loop
        End With
    End With
    Selection.Find.ClearFormatting
    Selection.Find.Replacement.ClearFormatting
    With Selection.Find
        .Text = "[Insert Title Appointed Person]"
        .MatchCase = True
        .Replacement.Text = "Chief Technology Officer"
    End With
    Selection.Find.Execute Replace:=wdReplaceAll
    Selection.Find.ClearFormatting
    Selection.Find.Replacement.ClearFormatting
    With Selection.Find
        .Text = "[Insert Title of `Appointed Person]"
        .MatchCase = True
        .Replacement.Text = "Chief Technology Officer"
    End With
    Selection.Find.Execute Replace:=wdReplaceAll
    Selection.Find.ClearFormatting
    Selection.Find.Replacement.ClearFormatting
        With Selection.Find
        .Text = "ADD DATE"
        .MatchCase = True
        .Replacement.Text = "November 9, 2018"
    End With
    Selection.Find.Execute Replace:=wdReplaceAll
    Selection.Find.ClearFormatting
    Selection.Find.Replacement.ClearFormatting

    With ActiveDocument.ActiveWindow.View
     .Type = wdPrintView
     .Zoom.Percentage = 250
    End With
End Sub

```
