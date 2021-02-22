
###########################################################################################################
### Lesson Objectives:
###			1) Create DOCKERFILE image running repo ngx_base (from git)
###			2) Start a Container from the projects/ngx_home image
###			3) Update the New Container NGINX_CUSTOM_HOME with some updates and new images.
###			4) Save new changes to a new Docker IMAGE (NGINX_CUSTOM_HOME_NEW)
###			5) Export the NGINX_CUSTOM_HOME_NEW as a DOCKERFILE
###			6) Create a new container based of image: NGINX_CUSTOM_HOME_NEW
###																									
###########################################################################################################

### USE DOCKERFILE FROM NGINX_CUSTOM_HOME ####
#1) Create DOCKERFILE image running repo ngx_base (from git)
root@containerhost:/home/instructor/projects/ngx_edt# git clone https://github.com/jcuel/ngx_home base
root@containerhost:/home/instructor/projects/ngx_edt# cd base/
root@containerhost:/home/instructor/projects/ngx_edt/base# docker build --tag="projects/ngx_home" /home/instructor/projects/ngx_edt/base/
root@containerhost:/home/instructor/projects/ngx_edt/base# docker image ls
REPOSITORY          TAG       IMAGE ID       CREATED              SIZE
projects/ngx_home   latest    e0e6c87f483a   About a minute ago   283MB

#2) Start a Container from the projects/ngx_home image
root@containerhost:/home/instructor/projects/ngx_edt/base# docker run -dp 80:80 projects/ngx_home
058dbd087cdc1db7d6b3102fb9a59ed024884574e0237acdbbbc66a76233984f
root@containerhost:/home/instructor/projects/ngx_edt/base# docker ps
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS          PORTS                NAMES
058dbd087cdc   projects/ngx_home   "nginx -g 'daemon of…"   20 seconds ago   Up 19 seconds   0.0.0.0:80->80/tcp   magical_bartik

#3) Update the New Container projects/ngx_home with some updates and new images.

