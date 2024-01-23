# About

Docker development setup for Prestashop 8.  

# Prerequisite

You'll need to clone and setup the development-kit package to set up your development environnement.

```
git clone https://github.com/neimheadh/development-kit.git
cd development-kit
bin/setup
```
Refer to the README for more info on how to use this kit.

# Services

## srvc_php
Loads up an php-fpm image with version 8.1 of PHP and version 8.0.4 of Prestashop
## srvc_nginx
Loads up an nginx image to serve the api  
The api's base url is https://prestashop.docker.localhost
## srvc_mariadb
Loads up mariadb
## srvc_pma
Loads up phpmyadmin  
Accessible on https://pma.prestashop.docker.localhost
## srvc_mail
Loads up maildev  
Accessible on https://mail.prestashop.docker.localhost


# Starting up

```
git clone https://github.com/henribaeyens/prestashop8-docker-setup.git
cd prestashop8-docker-setup
```
Check that the files in the bin directory are executable.  
Build the project using the following:

```
bin/build
```

# First install

The auto-install feature is disabled because it is not fully realiable. Do the following instead:  
Connect to the php container:
```
bin/bash
```
And run
```
bin/first-install
```
Before that, though, check the php container logs. Launch the script only if you see the following message:

> Reapplying PrestaShop files for enabled volumes ...  
> No pre-install script found, let's continue...  
> Almost ! Starting web server now  
> No init script found, let's continue...

Make sure the following folders exist:
- admin-dev
- install


# Reinstalling your shop

If you want to re-install your shop, run those

```
bin/stop
bin/clean
bin/build
bin/bash
```

Check that everything is ready (see **First install**) before launching the install script.
```
bin/first-install
```


