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

Check the php container logs. A successfull install should have produced the following output:
```
Checking if srvc_mariadb is available...
DB server srvc_mariadb is available, let's continue !
Setting up install lock file...
Reapplying PrestaShop files for enabled volumes ...
No pre-install script found, let's continue...
Renaming admin folder as admin-dev ...
Installing PrestaShop, this may take a while ...
Launching the installer script...
-- Installation successful! --
Removing install folder...
No post-install script found, let's continue...
Setup completed, removing lock file...
Almost ! Starting web server now
No init script found, let's continue...
```
  
# Reinstalling your shop

If you want to re-install your shop, run those

```
bin/stop
bin/clean
bin/build
```

# Back-office

Accessible at https://prestashop.docker.localhost/admin-dev  

>Email: admin@docker.local  
>Password: ShopAdmin!  

These credentials are set at build time. They can be changed by editing the docker-compose file.  

# Email configuration

Log into the back-office and head to  **Advanced parameters** > **Email**

Check the SMTP radio and enter the following information:

>SMTP server: srvc_mail  
>Encryption: none  
>Port: 25

Save and send a test email.  
Verify that it has properly been sent by going to https://mail.prestashop.docker.localhost

