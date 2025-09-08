---
title: Entra ID Connect Sync Issue - AADSTS700027
categories:
tags:
aliases:
share: true
---

Error message that is documented in MS Learn but without recommended solution - [Microsoft Entra authentication & authorization error codes | Azure Docs](https://docs.azure.cn/en-us/entra/identity-platform/reference-error-codes)

My homelab VM had a crash and I had to restore from snapshot, but in the process somehow the connect sync refuses to connect and throwing up error like below. I thought it would be easy fix, just reinstall the connect sync tool and move on. But, sadly it wasnt the case.
A configuration issue is preventing authentication - check the error message from the server for details. You can modify the configuration in the application registration portal. See [https://aka.ms/msal-net-invalid-client](https://aka.ms/msal-net-invalid-client "https://aka.ms/msal-net-invalid-client") for details. Original exception: AADSTS700027: The certificate with identifier used to sign the client assertion is expired on application. 

I was traversing the the internet without much luck, asked different forum and discord channels without any lead. 
I have uninstalled, reinstalled the connector too many times, deleted all the related registration apps, cleaned cache location, and I gave up. Weeks gone by without resolution and just by accident I needed to access files stored on the server and I went to connect to the SMB path \\servername\c$ and then browser to Users, I found my answer here. Each time it does uninstall and reinstall, it created a folder and thats where all the caches are stored in. 

I deleted it all and reinstalled the connector, it went successfully on the first attempt. 

![entra-connect-sync-users.png](/images/entra-connect-sync-users.png)