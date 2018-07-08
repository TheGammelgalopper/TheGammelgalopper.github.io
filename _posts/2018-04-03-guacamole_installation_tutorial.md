---
layout: post
title: Guacamole 0.9.13 Installation Tutorial
---

This has helped me getting a Guacamole installation up and running on a Ubuntu 16.04.3 LTS.

```
sudo apt-get update
sudo apt-get upgrade

apt -y install build-essential libcairo2-dev libjpeg-turbo8-dev libpng12-dev libossp-uuid-dev libavcodec-dev libavutil-dev libswscale-dev libfreerdp-dev libpango1.0-dev libssh2-1-dev libtelnet-dev libvncserver-dev libpulse-dev libssl-dev libvorbis-dev libwebp-dev mysql-server mysql-client mysql-common mysql-utilities tomcat8 freerdp ghostscript jq wget curl dpkg-dev

sudo nano /etc/default/tomcat8
//add these lines
# GUACAMOLE ENV VARIABLE
GUACAMOLE_HOME=/etc/guacamole
//ctrl+x,y, enter

//mysql new user and database
mysql -u root -p
//enter root %passwd%
CREATE USER 'guacadmin'@'localhost' IDENTIFIED BY 'guacadmin';
CREATE DATABASE guacamole_db;
GRANT ALL PRIVILEGES ON * . * TO 'guacadmin'@'localhost';
FLUSH PRIVILEGES;
quit

wget http://mirror.23media.de/apache/incubator/guacamole/0.9.13-incubating/source/guacamole-server-0.9.13-incubating.tar.gz
wget http://mirror.23media.de/apache/incubator/guacamole/0.9.13-incubating/binary/guacamole-0.9.13-incubating.war
wget http://mirror.23media.de/apache/incubator/guacamole/0.9.13-incubating/binary/guacamole-auth-jdbc-0.9.13-incubating.tar.gz
wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.43.tar.gz

tar -xzf guacamole-server-0.9.13-incubating.tar.gz
tar -xzf guacamole-auth-jdbc-0.9.13-incubating.tar.gz
tar -xzf mysql-connector-java-5.1.43.tar.gz

mkdir -p /etc/guacamole/lib
mkdir -p /etc/guacamole/extensions
cd guacamole-server-0.9.13-incubating
./configure --with-init-dir=/etc/init.d
make
sudo make install
sudo ldconfig
sudo systemctl enable guacd
cd ..

sudo mv -v guacamole-0.9.13-incubating.war /etc/guacamole/guacamole.war
sudo ln -s /etc/guacamole/guacamole.war /var/lib/tomcat8/webapps/
sudo ln -s /usr/local/lib/freerdp/guac*.so /usr/lib/x86_64-linux-gnu/freerdp/
sudo cp -v mysql-connector-java-5.1.43/mysql-connector-java-5.1.43-bin.jar /etc/guacamole/lib/
sudo cp -v guacamole-auth-jdbc-0.9.13-incubating/mysql/guacamole-auth-jdbc-mysql-0.9.13-incubating.jar /etc/guacamole/extensions/

sudo nano /etc/guacamole/guacamole.properties
//add these lines
mysql-hostname: localhost
mysql-port: 3306
mysql-database: guacamole_db
mysql-username: guacadmin
mysql-password: guacadmin
//ctrl+x,y, enter

rm -rf /usr/share/tomcat8/.guacamole
sudo ln -s /etc/guacamole /usr/share/tomcat8/.guacamole

service tomcat8 restart

cat guacamole-auth-jdbc-0.9.13-incubating/mysql/schema/*.sql | mysql -u root -p'passwd' guacamole_db
```

Webinterface login with guacadmin/guacadmin on IP:8080/guacamole

You can setup your connections under "Settings". If you are connected, press "Shift+Ctrl+Alt" to go to the settings of the current connection.
