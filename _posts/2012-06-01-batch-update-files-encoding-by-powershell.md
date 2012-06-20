---
layout: post
title: "batch update files encoding by powershell"
description: ""
category: PowerShell
tags: [powershell]
---
{% include JB/setup %}

<img width="200" src="http://ww4.sinaimg.cn/bmiddle/43a39d58gw1du4jhvqbjcg.gif" />

## how to update files encoding by powershell
---
	Get-ChildItem -Recurse | ForEach-Object{
		$outputName=$_.FullName
		Write-Host($outputName)
		if((Test-Path $_.FullName) -and ($_.Extension -ne "") -and ($_.Extension -ne ".ps1")){
			$contentValue=Get-Content -Encoding "UTF8" -Path $outputName
			Set-Content -Encoding "UTF8" -Path "$outputName" -value $contentValue
			Write-Host "update success"
		}
	 }
