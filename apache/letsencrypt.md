# Apache : Ajouter un domaine avec un support Letsencrypt

Tuto réalisé sur une debian

## Installation des packages

apt update
apt install -y apache2
a2enmod ssl rewrite

## Ajout du virtualhost

vim /etc/apache2/sites-enabled/www.mondomaine.tld.conf
````
<VirtualHost *:80>
    ServerAdmin contact@mondomaine.tld
    ServerName www.mondomaine.tld
    DocumentRoot /var/www/www.mondomaine.tld
    ErrorLog ${APACHE_LOG_DIR}/www.mondomaine.tld.error.log
    CustomLog ${APACHE_LOG_DIR}/www.mondomaine.tld.access.log combined
        
</VirtualHost>
````

## Ajout du user 

adduser www-mondomaine

Adapter le fichier : vim /etc/pasword
````
www-mondomaine:x:1001:1001:,,,:/var/www/www.mondomaine.tld:/usr/sbin/nologin
````

mkdir -p /var/www/www.mondomaine.tld

## Création d'un test

vim /var/www/www.mondomaine.tld/index.html
````
<html>
<body>
<h1>Yes ! Yes ! You're welcome to www.mondomaine.tld</h1>
</body>
````

chown www-mondomaine.www-mondomaine /var/www/www.mondomaine.tld -R

sudo systemctl reload apache2

## Installation de Letsencrypt avec Certbot

apt install -y snapd
snap install core; snap refresh core
snap install --classic certbot
ln -s /snap/bin/certbot /usr/bin/certbot

## Création du certificat

certbot --apache -d www.mondomaine.tld

## Renouvellement automatique du certificat

crontab -e
````
43 6 * * 0 certbot renew --post-hook "systemctl reload apache2" --quiet
````

## Effectuer un test SSL
https://www.ssllabs.com/ssltest/analyze.html?d=web%2d3.cloud.mondomaine.tld&latest