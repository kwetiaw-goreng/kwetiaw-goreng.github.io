---
title: How to re-organise exisiting Sensitivity Labels in Microsoft Purview
categories:
  - 
tags:
  - 
aliases: 
share: true
---

Tags: [howto]({{< ref "howto" >}}) [purview]({{< ref "purview" >}}) [microsoft365]({{< ref "microsoft365" >}})

Make sure that the Parent label is not scoped for Meetings, it doesnt work (as of 08/08/2024)

```
Connect-ExchangeOnline
Connect-IPPSSession -UserPrincipalName fahdy@doesthings.onmicrosoft.com
```

List all the labels to make sure it's connected successfully

```
Get-Label
```

Get the parent label immutable id

```
get-label -Identity 'Unofficial Parent' | select immutableid
```

Set the label to the parent

```
set-label -Identity 'Unofficial Baby' -ParentId 'the_immutable_id'
```

If you are getting this error message about invalid range

![SL_label_priority_invalid_range.png](/images/SL_label_priority_invalid_range.png)

First, change the parent to be the lower priority, for example priority 0

![SL_Labels_with_sublabels.png](/images/SL_Labels_with_sublabels.png)

Once you have all your sublabels set, you may wish to re-prioritise the label accordingly to your requirements

# References

[Set-Label (ExchangePowerShell) | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/exchange/set-label?view=exchange-ps)

[Connect to Security & Compliance PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/exchange/connect-to-scc-powershell?view=exchange-ps)

[Move AIP sublabels to a different parent label - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/move-aip-sublabels-to-a-different-parent-label/m-p/2113853)
