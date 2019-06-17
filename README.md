# dockerfiles
This repository contains some Dockerfiles for building Docker images:


- php-fpm-nginx-alpine: 
   This folder contains Dockerfile based on php5.6-fpm-alpine docker image, nginx is installed and 
   connects to fpm with unix socket instead of tcp socket.
   supervisor runs nginx and fpm in container.
   also there is a "conf" folder which contains nginx, fpm and supervisor configs.
   by default port 80 shows up php config page.
   
   
- nodejs: 
   This Dockerfile is based on node:8-alpine, pm2 and build dependencies are installed, 
   if you want use this dockerfile I recommend remove build dependecies after npm install to reduce docker image size. 
   ``` Run apk del .build-dependencies ```
   
   
- nodejs-no-builddep: 
   same as nodejs Dockerfile but without build dependecies
