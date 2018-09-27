# Horde_openSUSE_tumbelweed-nodejs
This container includes a runnable git checkout of Horde 5.
Additionally this container provides some more development tools like nodejs, babel or the ndm package.
If you just looking for a runnable Horde 5 look here:
https://build.opensuse.org/package/show/isv:B1-Systems:Horde5:containers:openSUSE:tumbleweed/horde5-developer

This container is designed for interactive development and testing of libraries both from upstream and from custom projects.

After cloning this repository you can run the following command:
docker-compose -f docker-compose.yml up
This should take a while.

Now you should be able to access the container with:

docker exec -it hordeOnTumbelweed_php_1 /bin/bash

Also you should be able to see the Horde environment via your browser on http://loacalhost 

To set up the database:

docker exec -it hordeOnTumbelweed_db_1 mysql -p -e "create database horde; grant all on horde.* to 'horde'@'%' identified by 'horde'";

docker exec -it hordeOnTumbelweed_php_1 chown wwwrun:www -R /srv/git/horde/base/config

Use the frontend for building the new configuration:
Go to the gear symbol select Administration->Configuration and then select the configuration for Horde.
    
Click on the database tab. Add the following settings:

SQL Database Settings:

$conf['sql']['phptype']    = MySQL/PDO
$conf['sql']['username']   = horde
$conf['sql']['password']   = horde
$conf['sql']['protocol']   = TCP/IP
$conf['sql']['hostspec']   = hordeOnTumbelweed_db_1
$conf['sql']['port']       = 3306
$conf['sql']['database']   = horde
$conf['sql']['charset']    = utf-8
$conf['sql']['ssl']        = No
$conf['sql']['splitread']  = Disabled
$conf['sql']['logqueries'] = no checkmark
    
Save the settings.
To finish the database setup run: 
docker exec -it hordeOnTumbelweed_php_1 /srv/git/horde/base/bin/horde-db-migrate-- 
Florian Frank
Linux Consultant & Trainer
Mobil: +49-151/42516532
Mail: frank@b1-systems.de

B1 Systems GmbH
Osterfeldstraße 7 / 85088 Vohburg / http://www.b1-systems.de
GF: Ralph Dehner / Unternehmenssitz: Vohburg / AG: Ingolstadt,HRB 3537 
