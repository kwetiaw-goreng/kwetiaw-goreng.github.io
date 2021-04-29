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

![Intune Portal](/assets/images/intune_scripts_3.png)

Review and Add > Save

![Intune Portal](/assets/images/intune_scripts_4.png)

Done!

This may take 15 minutes to take effect and few more minutes before it gets pushed to the end user devices.
You may force the devices to sync by going to **Windows Settings (WinKey + I)** > **Account** > **Access work or school** > **info** > press **Sync**

and see it in action from the log file located C:\ProgramData\Microsoft\IntuneManagementExtension\Logs\IntuneManagementExtension.log
Search for string [PowerShell]

That's it, I hope this will help tech out there!
