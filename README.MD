###########################################################################################################
# Lesson Objectives:
##			1) Create DOCKERFILE image running repo ngx_base (from git)
##			2) Start a Container from the projects/ngx_home image
##			3) Update the New Container NGINX_CUSTOM_HOME with some updates and new images.
##			4) Save new changes to a new Docker IMAGE (NGINX_CUSTOM_HOME_NEW)
##			5) Delete the Original Container
##																									
###########################################################################################################

* * USE DOCKERFILE FROM NGINX_CUSTOM_HOME * *

#1) Create DOCKERFILE image running repo ngx_base (from git)

```
root@containerhost:/home/instructor/projects/ngx_edt# git clone https://github.com/jcuel/ngx_home base
root@containerhost:/home/instructor/projects/ngx_edt# cd base/
root@containerhost:/home/instructor/projects/ngx_edt/base# docker build --tag="projects/ngx_home" /home/instructor/projects/ngx_edt/base/
root@containerhost:/home/instructor/projects/ngx_edt/base# docker image ls
REPOSITORY          TAG       IMAGE ID       CREATED              SIZE
projects/ngx_home   latest    e0e6c87f483a   About a minute ago   283MB

```
#2) Start a Container from the projects/ngx_home image

```
root@containerhost:/home/instructor/projects/ngx_edt/base# docker run -dp 80:80 projects/ngx_home
058dbd087cdc1db7d6b3102fb9a59ed024884574e0237acdbbbc66a76233984f
root@containerhost:/home/instructor/projects/ngx_edt/base# docker ps
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS          PORTS                NAMES
058dbd087cdc   projects/ngx_home   "nginx -g 'daemon of…"   20 seconds ago   Up 19 seconds   0.0.0.0:80->80/tcp   magical_bartik

```
#3) Update the New Container projects/ngx_home with some updates and new images.

```
root@containerhost:/home/instructor/projects/ngx_edt/www# docker cp index.html 058dbd087cdc:/var/www/html
root@containerhost:/home/instructor/projects/ngx_edt/www# docker cp ./img/logo6.jpg 058dbd087cdc:/var/www/html/img

```
#4) Save new changes to a new Docker IMAGE (NGINX_CUSTOM_HOME_NEW)

```
root@containerhost:/home/instructor/projects/ngx_edt/edited# docker commit 058dbd087cdc nginx_custom_home_new
sha256:f706fb5027283b0c026769ec30b600998d74d9a0fbd7324642520290cf103543
root@containerhost:/home/instructor/projects/ngx_edt/edited# docker images
REPOSITORY              TAG       IMAGE ID       CREATED             SIZE
nginx_custom_home_new   latest    f706fb502728   5 seconds ago       283MB
projects/ngx_home       latest    e0e6c87f483a   About an hour ago   283MB

```
#5) Delete the Original Container

```
root@containerhost:/home/instructor/projects/ngx_edt/edited# docker stop 058dbd087cdc
058dbd087cdc
root@containerhost:/home/instructor/projects/ngx_edt/edited# docker rm 058dbd087cdc
058dbd087cdc
root@containerhost:/home/instructor/projects/ngx_edt/edited# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```
