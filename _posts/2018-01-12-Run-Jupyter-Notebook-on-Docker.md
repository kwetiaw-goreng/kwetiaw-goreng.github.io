---
title: Run Jupyter Notebook in Docker
---

Quickly spin up Jupyter Notebook with this simple command.
Amend any one that is marked with a bracked <>. The web GUI then will be accessible on http://HOST_IP:11000

```docker
docker run –name=jupyter –restart=always -e NB_USER=<any_username> \
-e NB_UID=1000 –user=root -e CHOWN_HOME=yes -d -p 11000:8888 -e JUPYTER_LAB_ENABLE=yes \
-v <folder_location_on_host>:/home/<any_username>/work -e GRANT_SUDO=yes jupyter/datascience-notebook:137a295ff71b
````
