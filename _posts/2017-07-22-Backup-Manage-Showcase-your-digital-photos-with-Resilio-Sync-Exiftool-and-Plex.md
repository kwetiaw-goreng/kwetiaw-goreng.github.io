---
title: Backup > Manage > Showcase-your digital photos with Resilio Sync > Exiftool > and Plex
---


Backup, ugh…sounds boring.As a modern day photographer, having a proper backup of your digital photos is a must, but often being overlooked because, well it’s boring and time consuming.
I personally have tried several different methods but none of them really tick my boxes. I used to perform manual backup over network or via USB cable to my home NAS when I “remember” (Not good enough!). I have lost way too many important photographs because of this.

My requirements
1. Automatic backup – must! (from multiple sources ios, android, windows/mac/linux)
1. Automatic photo sorting – aint nobody got time for that
1. Consumption has to be easy and from anywhere and any device.

Resilio Sync is used here to automatically backup the photos on mobile devices or computer, Share the folder where your camera app saves the photo to and sync it up back to a temporary location on your NAS.
Exiftool is a very powerful utility that can be used to automatically sort your photos and videos based on the camera’s metadata information. Install exiftool on your NAS and lets do some sorting!

The code
```powershell
exiftool -r -ext mp4 -ext jpg '-Directory</final/destination/of/your/photos/$CreateDate' -d "%Y/%B" /location/of/your/temp/folder
````

Real Life Example
```powershell
exiftool -r -ext mp4 -ext jpg '-Directory</mnt/4tbexternal/docker/plex/plexmedia/photos/Fahdy Android/$CreateDate' -d "%Y/%B" /mnt/4tbexternal/docker/plex/plexmedia/photos/Fahdy\ Temp/
````

This line of code will rename, move and sort your photographs based on the metadata $CreateDate. The folder structure will look like this

![directory_tree](/assets/images/photodirectorytree.png)
