---
title: Running AdGuard Home on CHIP Computer
---
Installing AdGuard home in linux is as easy as executing this command line. Make sure to assign your CHIP a Static IP address on your router.

Open Terminal

Paste below
`curl -sSL https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh`

When successful, you will see something like below

![](/assets/images/adguard/adguard-chip.png)

Then navigate to the IP address of your CHIP or Raspberry Pi
![](/assets/images/adguard/adguard1.png)

Leave everything as is
![](/assets/images/adguard/adguard2.png)

Enter your preferred admin login 
![](/assets/images/adguard/adguard3.png)

Almost there, you can either set your DNS individually at device level or at router level.
![](/assets/images/adguard/adguard4.png)

Open dashboard
![](/assets/images/adguard/adguard5.png)

I used DDWRT firmware on my router, add your CHIP IP address to the Static DNS 1. Check your device manufacturer manual to figure out how to do this correctly, otherwise you will not be able to browse the web. Set 8.8.8.8 to the Static DNS 2, so in case your CHIP fails, it will use the 2nd DNS as alternative.
![](/assets/images/adguard/ddwrt_dns_settings.png)

Once set up, try navigating to a known website that has lots of intrusive Ads and you will be surprised to see how much faster your web page loads now.
![](/assets/images/adguard/adguard-test2.png)


