## Debian Jessie Vagrant Box

The Debian Jessie Vagrant Box project goal is simple. Create a Vagrant box pre-installed and configured with the most commonly used packages available. A list of pre-installed packages is listed within the Box Includes section of this file.

## Box Start

vagrant up

vagrant ssh

sudo service apache2 start

## Apache Setup

The pre-installed Apache package has been somewhat modified so that configuring new virtual hosts are easy

## User Accounts

All accounts including root accounts have the same password of "sinatra"

A user of "frank" is also available for use with the same password listed above.

## Box Includes
1. Apache 2.4
	1. Mod Rewrite: Enabled
	2. Mod PHP5: Installed
	3. Mod Security: Installed and configured
	4. Mod Evasive: Installed and configured
	5. SSL: Installed and configured
	6. SSL Certificates: Generated and configured
	7. Mod Python
	8. Mod Passenger
2. PHP 5.5
	1. MySQL Extension
	2. PostgreSQL Extension
	3. SQLite Extension
	4. Mcrypt Extension
	5. Sybase Extension
	6. ODBC Extension
	7. Curl Extension
	8. GD Extension
	9. Imagick Extension
	10. Memcache Extension
	11. XmlRPC Extension
	12. XSL Extension
	13. JSON Extension
	14. APC Extension
	15. Mongo Extension
3. MySQL Server
4. PostreSQL
5. Composer
6. OpenSSL
7. MongoDB
8. Git
9. Python
10. Node.js
	1. Gulp.js
11. Ruby
12. Rails
13. G++
14. Make