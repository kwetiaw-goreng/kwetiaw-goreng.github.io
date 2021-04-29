---
title: Push Registry Value Using PowerShell And Intune
---

Simple PowerShell script to update a registry key value

For example, script below is to update Adobe Acrobat DC defauly language to en_US 
````Set-ItemProperty -Path "HKLM:\SOFTWARE\WOW6432Node\Adobe\Adobe Acrobat\DC\Language" -Name '(Default)' -value 'en_US' ````

![Adobe Acrobat DC registry](/assets/images/registry_adobe.png)



