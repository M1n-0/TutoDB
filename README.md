# Tuto Base De Données

## Sommaire
- [Introduction](#introduction)
- [Installation](#installation)
- [Configuration](#configuration)
-  [Utilisation](#utilisation)

## Introduction
### Je vais vous montrer comment installer et faire une base de donnée ainsi que de pouvoir récupérer des informations de cette base de donnée.
### Cela se fera uniquement en ligne de commande et je vais utiliser notre cas de base de donnée donc le systeme d'exploatation utilisé sera Raspbian donc Debian pour Raspberry Pi.(casiment toute les commandes sont similaire pour Debian et Ubuntu et certain comme les ``apt`` de ``sudo apt install`` )

## Installation

### En 1er on va vérifier si on a pas des maj à faire sur notre système
```bash
sudo apt update
sudo apt upgrade
```
### Ensuite on va installer notre base de donnée
```bash
sudo apt install mariadb-server
```
### Et c'est tout pour l'installation :D

## Configuration

### La configuration va être plus longue mais pas compliqué (pas pour tout le monde hein((apres y a mes mp 😊 )) )

### Dès que vous avez installer mariadb-server on va devoir la configurer ça base :
```bash
sudo mysql_secure_installation
```
### Ca va vous affichier ceci :
```
nino@raspberrypi:~ $ sudo mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n]
```
### Si vous avez pas de mot de passe pour root appuyer sur ``n`` sinon mettez le mot de passe de votre choix.

<br>

### Ensuite il va vous demander si vous voulez garder le user anonyme creer de base pour maria db que tout le monde peux utiliser, perso je l'ai enlever mais la c'est votre choix.

<br>

### Dans le suite du tuto on va creer user pour la db donc on peux le supprimer :)

```bash
By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n]
```
### La on met `Y` (stp)

<br>

### Ensuite il va vous demander si vous voulez que le root puisse se connecter que en localhost, perso je l'ai mis en `N` car on va creer des user spécifier apres. (utiliser ssh sur les serveur pour la db comme ça le root reste sécu)

```bash
Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n]
```
### Toujours `Y` pas très compliquer j'ai dit hein ??

### Ensuite il va vous demander si vous voulez supprimer la base de donnée de test, perso je l'ai fait car beh on s'en fout de ça DB test.

```bash
By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n]
```
### Devinez quoi toujours : `Y` Trop dur je sais 

### Ensuite il va vous demander de recharger les privilèges de la db, bah on va pas dire non hein

```bash
Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n]
```
### `Y` encore et encore

### Tada la configuration initiale de maria-db est fini j'ai pas menti c'était pas compliquer hein ??

## Utilisation

### Pour utiliser maria-db on va utiliser le user root car comme ça grace a cette magnifique configuration on peux se connecter sans mettre un mdp différent juste celui du user root de ta machine (si tu suis se beau tuto)

```bash
sudo mysql -u root -p
```

### Donc tu va passer de ça :
```bash
nino@raspberrypi:~ $ 
```
### A ça :
```bash
MariaDB [(none)]>
```
### C'est normal tkt pas, bref mtn on va creer notre DB (le nom va être ladbd pour le tuto mais tu peux mettre ce que tu veux) :
    
```sql
MariaDB [(none)]> CREATE DATABASE ladbd;
```

### Juste apres ça vu que c'est tout frais on va creer un user pour la db:
```sql
MariaDB [(none)]> CREATE USER 'user'@'localhost' IDENTIFIED BY 'mdp';
```
### Ok par contre la le user à login que en localhost donc si tu veux qu'il puisse se connecter de partout tu peux mettre `@'%'` a la place de `@'localhost'` c'est kdo

### Ensuite on va donner les droits a notre user sur la db qu'on a creer :
```sql
GRANT ALL PRIVILEGES ON ladb.* TO 'nino'@'localhost';
```
### Même chose que pour le user si tu veux qu'il puisse se connecter de partout tu peux mettre `@'%'` a la place de `@'localhost'`

### Et pour appliquer tout ces changements :
```sql
FLUSH PRIVILEGES;
```

### Et voila vous avez une base de donnée avec un user et tout et tout, mtn si vous voulez Faire des trucs dessus vous avez juste a faire des requetes SQL apres avec fait : 
```sql
USE ladbd;
```
### Maria-db va changer de ça :
```sql
MariaDB [(none)]> 
```
### A ça :
```sql
MariaDB [ladbd]> 
```
### Et voila vous pouvez faire vos requetes SQL comme `CREATE TABLE`, `INSERT INTO`, `SELECT * FROM` etc...
<br>
<br>

# Have Fun 😊