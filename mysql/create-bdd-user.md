# Mysql : Création d'un utilisateur et de sa base de données

Se connecter à la base est lancer les commandes suivants.  
Attention aux valeurs à personnaliser : bdd, username, password

````
CREATE DATABASE bdd;
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON bdd.* TO 'username'@'%';
FLUSH PRIVILEGES;
````