# Blog de Yannick LALLEAU

## Prestashop : Ajouter le support de l'extension image Jfif / Jpeg dans les images de produit

Manipulation réalisation sur la version de PrestaShop : 1.7.8.5  

Modifier les fichiers suivants :  

- **/controllers/admin/AdminProductsController.php:2819**  
 Avant :  
  $image_uploader->setAcceptTypes(['jpeg', 'gif', 'png', 'jpg'])->setMaxSize($this->max_image_size);  
 Après :   
  $image_uploader->setAcceptTypes(['jpeg', 'jfif', 'gif', 'png', 'jpg'])->setMaxSize($this->max_image_size);  
- **/classes/ImageManager.php:448**  
  - Avant :  
  $authorizedExtensions = ['gif', 'jpg', 'jpeg', 'jpe', 'png'];  
  - Après :  
  $authorizedExtensions = ['gif', 'jpg', 'jpeg', 'jpe', 'png', 'jfif'];

## LetsEncrypt : Ajouter un nouveau nom de domaine sur Apache

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

## Apache : Profiter de php fpm sur un virtualhost

Editer le fichier virtualhost du domaine concerné et ajouter les lignes suivantes:
```
<FilesMatch \.php$>
  SetHandler "proxy:unix:/run/php/php7.4-fpm.sock|fcgi://localhost"
</FilesMatch>
```
La version de php dans cet exemple est la 7.4 