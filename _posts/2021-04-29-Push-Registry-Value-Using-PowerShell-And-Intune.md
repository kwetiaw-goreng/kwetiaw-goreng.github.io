---
title: Push Registry Value Using PowerShell And Intune
---

Simple PowerShell script to update a registry key value

For example, script below is to update Adobe Acrobat DC defauly language to en_US 
````Set-ItemProperty -Path "HKLM:\SOFTWARE\WOW6432Node\Adobe\Adobe Acrobat\DC\Language" -Name '(Default)' -value 'en_US' ````

![Adobe Acrobat DC registry](/assets/images/registry_adobe.png)

Create your .ps1 file with the desired command and lets upload it to Microsoft Intune (Microsoft Endpoint Manager)

In your Intune portal, go to **Devices** > **Scripts** > click **Add** > select **Windows 10**

![Intune Portal](/assets/images/intune_scripts.png)

Add the relevant information, if PS script is not too long, you can paste it in the description box for easier future re-use

![Intune Portal](/assets/images/intune_scripts_1.png)

Select Yes on **Run Script in 64 bit PowerShell Host**

![Intune Portal](/assets/images/intune_scripts_2.png)

Add the target groups
