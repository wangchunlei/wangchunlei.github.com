---
layout: post
title: "batch update files encoding by powershell"
description: ""
category: PowerShell
tags: [powershell]
---
{% include JB/setup %}

## how to update files encoding by powershell
{% highlight ruby %}
Get-ChildItem -Recurse | ForEach-Object{
    $outputName=$_.FullName
    Write-Host($outputName)
    if((Test-Path $_.FullName) -and ($_.Extension -ne "") -and ($_.Extension -ne ".ps1")){
        $contentValue=Get-Content -Encoding "UTF8" -Path $outputName
        Set-Content -Encoding "UTF8" -Path "$outputName" -value $contentValue
        Write-Host "update success"
    }
 }
{% endhighlight %}