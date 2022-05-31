# Apache : Ajouter un certificat sur nouveau nom de domaine / virtualhost

Créer le virtualhost :  
**vim /etc/apache2/site-enabled/www.mondomaine.tld.conf**
```
<VirtualHost *:80>
    ServerAdmin contact@mondomaine.tld
    ServerName www.mondomaine.tld
    
	DocumentRoot /var/www/www.mondomaine.tld

	<Directory /var/www/www.mondomaine.tld>
		AllowOverride All
		Options -Indexes
	</Directory>

    ErrorLog ${APACHE_LOG_DIR}/error-mondomaine.tld.log
    CustomLog ${APACHE_LOG_DIR}/access-mondomaine.tld.log combined
</VirtualHost>

<VirtualHost *:80>
    ServerName mondomaine.tld
    RedirectMatch permanent ^/(.*) https://www.mondomaine.tld/$1
</VirtualHost>
```

Ensuite lancer la commande :
**certbot --apache www.mondomaine.tld**

Un nouveau fichier est créé :
/etc/apache2/sites-enabled/www.mondomaine.tld-le-ssl.conf