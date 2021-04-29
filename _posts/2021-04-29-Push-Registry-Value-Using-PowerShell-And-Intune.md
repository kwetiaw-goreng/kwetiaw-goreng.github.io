---
title: Push Registry Value Using PowerShell And Intune
---

Simple PowerShell script to update a registry key value

````Set-ItemProperty -Path "HKLM:\SOFTWARE\WOW6432Node\Adobe\Adobe Acrobat\DC\Language" -Name '(Defaukt)' -value 'en_US' ````

