---
title: Docker on Raspberry Pi 3
---

Docker now runs on Raspberry Pi!
Follow this [guide](https://www.raspberrypi.org/blog/docker-comes-to-raspberry-pi/) to install it on your Pi – Docker Raspberry Pi
Or enter this one liner – curl -sSL https://get.docker.com | sh

Note, only container that was built specifically to run on armhf board will run on Raspberry Pi. Google keyword searches should include armhf, docker, raspberry pi

Containers running on my Pi3?
    *MariaDB (Database)
    *MQTT (Location Tracking to be used alongside of HomeAssistant)
    *NGINX with LetsEncrypt (Reverse Proxy to allow secure access to my internal services without having to port forward all the required ports)
    *Resilio Sync (File Sharing/Cloud)
    *Portainer (GUI interface to manage the containers)
    *Organizr (Web Portal allowing easy access to my services)
    *HASS (Home Automation Software)

Other services that are not in containers
    *Webmin
    *SSH Server (Tunnel service while at work)

I need the services above to run 24×7 and this is why Raspberry Pi fits the bill (I dont like seeing a fat electricity bill). To run a pi for the entire year will cost somewhere between $3-5 (varies of course)
I need my documents all the time and resilio sync allows me to access my files from everywhere. I need my KeePass password book, lets be honest, we dont remember all the passwords and PINs and other security numbers.
I love my home automation and I love HomeAssistant, it’s just RAD! Home automation that doesnt run 24×7 is pretty useless dont you think?
I also need to be able to securely access my home network from work, secure SOCKS5 SSH tunnel does the job!
Here’s a high level overview of the setup

Additional hardware attached to the rPI
    *USB 3.0 Stick 64GB (data storage for resilio sync)
    *Home made RF Transceiver (to control RF enabled power outlets)

Once you have prepared your Raspberry Pi with Docker, I recommend that you check out this Linux Server IO list of docker containers and make sure to select the armhf repository.
Let’s do an example – Resilio Sync
I have 64GB USB stick connected and mapped to /mnt/USB64GBstick/ and I usually create seperate folder for each of the services to avoid unwanted behaviour. You dont need to create the folder manually, docker will do it on your behalf. Notice on the below command, the -v flag will map host folder to the container. So what you create /mnt/USB64GBstick/resilio/config will correspond to /config inside the container

```docker
docker run -d \
--name=resilio-sync \
-v /mnt/USB64GBstick/resilio/config:/config \
-v /mnt/USB64GBstick/resilio/sync:/sync \
-e PGID=1000 -e PUID=1000 \
-p 8888:8888 \
-p 55555:55555 \
lsioarmhf/resilio-sync
````

Copy and paste the above command and your container will be ready in no time. If the system does not spit any error message, most likely your container is now ready to be used. Point your browser to your Raspberry Pi IP Address http://rpi.ipaddress:8888 and you shall be greeted to set up Resilio Sync for the first time.
Pro Tip – I typically add a line --restart=always to each of my container that I need it to start automatically after each host reboot or recovery from power failure, etc.

docker run -d \
--name=resilio-sync \
--restart=always \
-v /mnt/USB64GBstick/resilio/config:/config \
-v /mnt/USB64GBstick/resilio/sync:/sync \
-e PGID=1000 -e PUID=1000 \
-p 8888:8888 \
-p 55555:55555 \
lsioarmhf/resilio-sync

That’s it, now you can start experimenting with different services that potentially can save you money and be less reliant of the 3rd party that often sell your information to other 3rd party. Note: resilio sync is not an OSS (open source software) and I am awaiting Syncthing to allow selective folder sync before moving away from resilio sync.
Here’s few ideas to get you started
*Have your files everywhere – [Syncthing](https://hub.docker.com/r/lsioarmhf/syncthing)
*Have your own spotify with – [Libre Sonic](https://hub.docker.com/r/lsioarmhf/libresonic)
*Run your own ebook library, because why not? – [ubooquity](https://hub.docker.com/r/lsioarmhf/ubooquity/)
*Have fun!
