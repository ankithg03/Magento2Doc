# Magento2Doc
﻿## Installation
## Install Apache2
Apache2 installation
```
sudo apt update
sudo apt install apache2
sudo systemctl enable apache2.service
```
Enabling mod_rewrite
		
	sudo a2enmod rewrite
	sudo systemctl restart apache2

Enable rewrite engine for html

	sudo nano /etc/apache2/sites-available/000-default.conf
```bash
<VirtualHost *:80>
    <Directory /var/www/html>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All## Install Apache2 PHP and Required Extensions

        Require all granted
    </Directory>

    . . .
</VirtualHost>
```
	sudo systemctl restart apache2

	sudo nano /var/www/html/.htaccess
```bash
#content
RewriteEngine on
```

## Instal PHP and Required Extensions
	sudo apt install php7.4 libapache2-mod-php7.4 php7.4-common php7.4-gmp php7.4-curl php7.4-soap php7.4-bcmath php7.4-intl php7.4-mbstring php7.4-xmlrpc php7.4-mcrypt php7.4-mysql php7.4-gd php7.4-xml php7.4-cli php7.4-zip
## Installation of Mysql
	sudo apt install mysql-server
	sudo mysql_secure_installation
Creating a new user
	
	mysql> CREATE USER 'magento'@'localhost' IDENTIFIED BY 'magento';
	mysql> GRANT ALL PRIVILEGES ON *.* TO 'magento'@'localhost''
	mysql> FLUSH PRIVILEGES;
## Install Composer 
		
	curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer

Note: Provide permission to your mageno2 directory
```
sudo chown -R www-data:www-data /var/www/html/magento2/
sudo chmod -R 755 /var/www/html/magento2/
```

## Install Elasticsearch
	sudo apt install -y apt-transport-https openjdk-8-jre-headless
	wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
	echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-6.x.list
	sudo apt update && sudo apt install -y elasticsearch
	sudo /bin/systemctl daemon-reload
	sudo /bin/systemctl enable elasticsearch.service
	sudo systemctl start elasticsearch.service
	sudo systemctl status elasticsearch.service
	echo "Waiting for ElasticSearch to boot up..."
	sleep 20
	curl -XGET 'localhost:9200/?pretty'
## Magento 2 Installation
	 composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition <install-directory-name>
	 example: 
	 composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
	 
	 cd /var/www/html/<magento install directory>  find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
	 find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} + chown -R :www-data . #  Ubuntu
	 chmod u+x bin/magento
	 
 **Installation**
 
	bin/magento setup:install \
	--base-url=http://127.0.0.1/magento2 \
	--db-host=localhost \
	--db-name=magento \
	--db-user=magento \
	--db-password=magento \
	--admin-firstname=admin \
	--admin-lastname=admin \
	--admin-email=admin@admin.com \
	--admin-user=admin \
	--admin-password=admin123 \
	--language=en_US \
	--currency=INR \
	--timezone=Asia/Kolkata \
	--use-rewrites=1
