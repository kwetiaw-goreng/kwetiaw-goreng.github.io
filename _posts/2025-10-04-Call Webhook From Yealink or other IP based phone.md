---
title: Call Webhook From Yealink or other IP based phone
categories:
tags:
aliases:
share: true
---
# 2025-10-04-Call Webhook From Yealink or other IP based phone
I recently acquired a Yealink handset (Prime Business Phone SIP-T54W) with the intention to set up a cost effective home phone to be used for emergency situation. My daughters are too young to have their own mobile phones so if I am at the office and if in case of emergency, they know that they can use this phone to call me or other emergency services. 
The VOIP provider that I use is CrazyTel and you can get started with them for cheap on their PAYG plan and they even give you a $2 credit to get you started.

You can get connected under 5 minutes, copy and paste login information to the phone and you will be calling in no time.
With Yealink, go to the IP address of the phone from a web browser, default administrator login is admin:admin. Once logged in, head to Account > Register and enter the connection credentials and SIP server here and press confirm, if all goes well, it will show that you have been successfully registered.

Setting up speed dial is from DSSkey menu > Line Key.

Now, assuming you have HomeAssistant or N8N or any service that can accept webhook as a trigger, you could do some cool stuff with it.
For example in HomeAssistant, you can set up an automation that uses a webhook as trigger and your imagination is the limit here on what you can do. Turn a light switch on or off? sure! Play music? lets groove! play an announcement to your smart speakers! time for dinner!

A very simple automation that just sends notification to my mobile
![webhook-hass.png](/images/webhook-hass.png)

Once you have saved the automation, you will be able use this URL as the webhook url - YOUR-HASS-URL/api/webhook/test-yealink

Copy the URL and head to Yealink web GUI > Dsskey > Line Key > change the type to XML Browser and paste the URL > confirm to save
![yealink-xml-browser-webook.png](/images/yealink-xml-browser-webook.png)

Now on your handset, pressing Speed Dial 8 will trigger the automation.

![hass-webhook-telegram-notify.jpg](/images/hass-webhook-telegram-notify.jpg)

Happy calling!