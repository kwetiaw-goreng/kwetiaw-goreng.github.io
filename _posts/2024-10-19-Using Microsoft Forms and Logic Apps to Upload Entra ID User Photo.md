---
title: Using Microsoft Forms and Logic Apps to Upload Entra ID User Photo
categories:
  - 
tags:
  - 
aliases: 
share: true
---

Create Microsoft Forms with at least 2 questions, you may add some more depending on your requirement

My form only uses 2 questions, UserPrincipalName (Email) and the attachment question

![forms-user-photo-upload.png](/images/forms-user-photo-upload.png)

Here's the designer view of the logic app

![forms_user_photo_upload_la.png](/images/forms_user_photo_upload_la.png)

Make sure to use Managed Identity for better security and less overhead and it needs at least `User.ReadWrite.All`

It's so easy to extend what the logic app can do after a successful run, you could archive the photo to different folder depending on the outcome of the run, you could add notification to relevant people/team, etc.
