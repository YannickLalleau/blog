## Apache : Profiter de php fpm sur un virtualhost

Editer le fichier virtualhost du domaine concerné et ajouter les lignes suivantes:
```
<FilesMatch \.php$>
  SetHandler "proxy:unix:/run/php/php7.4-fpm.sock|fcgi://localhost"
</FilesMatch>
```
La version de php dans cet exemple est la 7.4 