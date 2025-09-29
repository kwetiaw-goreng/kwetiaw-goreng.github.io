---
title: Run a local ebook webserver for old reader
categories:
tags:
aliases:
share: true
---
If you have an old e-reader with wifi and web browser like one I have Sony PRS-T2. The web browsers no longer able to load secure websites as it is an end of life product and no longer receiving updates. 
Since I have a linux server running docker, it dawned on me that I could just run a docker webserver using apache or nginx to serve directory containing any kind of files, in my case, ebook files. That's exactly what I did and you could do the same by running this command, update the port accordingly.

```
docker run -d --name ebook-server -p 8057:80 -v /path/to/local/files:/usr/local/apache2/htdocs/ httpd:latest
```

![ebook-server.png](/images/ebook-server.png)

Now if you are lucky, your outdated web browser in your ebook reader might be able to open this site and download directly to the device. 

![sony-prs-t2.jpg](/images/sony-prs-t2.jpg)