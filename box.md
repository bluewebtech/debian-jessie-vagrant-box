## Project Vagrant Debian Jessie Project

The following instructions describe the complete process that was involved in creating the debian-jessie-vagrant-box.box, that is available for download at https://www.dropbox.com/s/co1t7apq03jb1la/debian-jessie-vagrant-box.box.

### Initial setup

	cd C:/VagrantBoxes

	mkdir DebianJessie

	cd DebianJessie

	vagrant box add DebianJessie https://downloads.sourceforge.net/project/vagrantboxjessie/debian80.box

	vagrant init DebianJessie

	vagrant ssh-config

	vagrant up

	vagrant ssh

### Root config

	su passwd <password>

## Software Installation

### Update system
	
	sudo apt-get update

### Apache Installation
	
	sudo apt-get install apache2
	
	sudo a2enmod rewrite
	
	a2enmod headers
	
	sudo apt-get install libapache2-mod-php5 libapache2-modsecurity libapache2-mod-evasive
	
	sudo a2enmod evasive

	<VirtualHost *:80>
		ServerAdmin webmaster@localhost
		DocumentRoot /vagrant/apache/www/dev.vagrant
		DirectoryIndex index.php
		ServerName dev.vagrant
		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>

	<VirtualHost *:80>
		ServerName dev-ssl.vagrant
		Redirect permanent / https://dev-ssl.vagrant/
	</VirtualHost>

	<VirtualHost *:443>
		SSLEngine on
		SSLCertificateFile /vagrant/apache/ssl/vagrant.cert
		SSLCertificateKeyFile /vagrant/apache/ssl/vagrant.key
		ServerAdmin webmaster@localhost
		DocumentRoot /vagrant/apache/www/dev-ssl.vagrant
		DirectoryIndex index.php
		ServerName dev-ssl.vagrant
		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>

	sudo service apache2 restart

### PHP Installation
	
	sudo apt-get install php5 php5-mysql php5-pgsql php5-sqlite php5-mcrypt php5-sybase php5-odbc php5-curl php5-gd php5-imagick php5-
	memcache php5-xmlrpc php5-xsl php5-json php-apc php5-mongo
	
	sudo nano /etc/php5/apache2/php.ini
	
	Change expose_php Off to expose_php On

### OpenSSL Installation
	
	sudo apt-get install openssl
	
	sudo a2enmod ssl
	
	sudo a2ensite default-ssl
	
	openssl req -new -out vagrant.csr -keyout vagrant.pem

	Answer the following questions:
	
	1. Enter a pass phrase: sinatra
	2. Verify - Enter PEM pass phrase: sinatra
	3. Country Name (2 letter code) [AV]: US
	4. State or Province Name (full name) [Some-State]: New York New York
	5. Locality Name (eg. city) []: New York New York
	6. Organization Name (eg. company) [Internet Widgets Pty Ltd]: Angel Eyes
	7. Organizational Unit Name (eg. section) []: AE
	8. Common Name (e.g. server FQDN or YOUR name) []: *.vagrant
	9. Email Address []: frank.sinatra@foo.com
	10. Please enter the following 'extra' attributes to be sent with your certificate request.
	11. A challenge password []:
	12. A optional company name []:

	openssl rsa -in vagrant.pem -out vagrant.key
	
	openssl x509 -in vagrant.csr -out vagrant.cert -req -signkey vagrant.key -days 3650

### MySQL Installation
	
	sudo apt-get install mysql-server

### MySQL Workbench Connection
	1. Connection Method: Standard TCP/IP over SSH
	2. SSH Hostname: 192.168.33.10:22
	3. SSH Username: vagrant
	4. SSH Key File: ex: C:\Users\<username>\.vagrant.d\insecure_private_key
	5. MySQL Hostname: 127.0.0.1
	6. MySQL Server Port: 3306
	7. Username: root
	8. Password: <password>

### PostgreSQL Installation
	
	sudo apt-get install postgresql
	
	sudo passwd postgres
	
	cd /etc/postgresql/9.3/main
	
	sudo nano pg_hba.conf

	Add the following:
	host    all             all             192.168.33.10/24        trust
	under:
	host    all             all             127.0.0.1/32            md5
	result:
	host    all             all             127.0.0.1/32            md5
	host    all             all             192.168.33.10/24        trust

	sudo nano postgresql.conf

	Update the following:
	
	#listen_addresses = 'localhost'  # what IP address(es) to listen on;
	
	to:
	
	listen_addresses = '*'  # what IP address(es) to listen on;

	sudo service postgresql restart

### Install MongoDB
	
	sudo apt-get install mongodb

### Install Composer
	
	su <password>
	
	curl -sS https://getcomposer.org/installer | php
	
	mv composer.phar /usr/local/bin/composer

### Git Installation
	
	sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev build-essential
	
	sudo apt-get install git

### Python Installation
	
	sudo apt-get install python libapache2-mod-python

### Node.js Installation
	
	sudo apt-get install nodejs
	
	sudo apt-get install npm

### Ruby Installation
	
	sudo apt-get install ruby build-essential libapache2-mod-passenger rdoc ruby-dev rubygems
	
	gem install fastthread
	
	sudo gem install rails
	
	sudo gem install sass
	
	sudo gem install compass

### G++ and Make Installation
	
	sudo apt-get g++ make