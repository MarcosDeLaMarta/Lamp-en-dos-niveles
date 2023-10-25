# **LAMP en dos niveles**
#### Marcos de la Marta Núñez

<br />
<br />

 <img src="Img/lamp.png" width="400" height="250">

 <br />
<br />
<br />
<br />

# Índice

# Índice


1. [**1. Creación y configuración de las máquinas**](#1-creación-y-configuración-de-las-máquinas)
    1. [Creación de las máquinas en Vagrant](#creación-de-las-máquinas-en-vagrant)
        - [Vagrantfile de las dos máquinas](#vagrantfile-de-las-dos-máquinas)
    2. [Scripts de aprovisionamiento](#scripts-de-aprovisionamiento)
        - [Script para el servidor Apache](#script-para-el-servidor-apache)
        - [Script para el servidor MySQL](#script-para-el-servidor-mysql)
2. [**2. Configuración servidor MySQL**](#2-configuración-servidor-mysql)
    - [Clonar la carpeta de GitHub en la máquina SQL](#clonar-la-carpeta-de-github-en-la-máquina-sql)
    - [Modificar el fichero 50-server.cnf](#modificar-el-fichero-50-servercnf)
    - [Ejecutar el Script SQL en el servidor](#ejecutar-el-script-sql-en-el-servidor)
    - [Crear un usuario de MySQL con la IP del servidor Apache](#crear-un-usuario-de-mysql-con-la-ip-del-servidor-apache)
3. [**3. Configuración servidor Apache**](#3-configuración-servidor-apache)
    - [Mover archivos a /var/www](#mover-archivos-a-varwww)
    - [Crear un fichero de configuración en sites-available](#crear-un-fichero-de-configuración-en-sites-available)
    - [Editar el fichero de configuración](#editar-el-fichero-de-configuración)
    - [Habilitar el fichero de configuración](#habilitar-el-fichero-de-configuración)
    - [Desactivar el fichero de configuración anterior](#desactivar-el-fichero-de-configuración-anterior)
    - [Editar el archivo config.php](#editar-el-archivo-configphp)
    - [Ingresar al servidor MySQL desde el servidor Apache](#ingresar-al-servidor-mysql-desde-el-servidor-apache)
    - [Verificar el resultado](#verificar-el-resultado)

<br />
<br />
<br />
<br />
<br />
<br />
<br />

## [**1. Creación y configuración de las máquinas**](#1-creación-y-configuración-de-las-máquinas)
<br />
<br />

### Creamos dos máquinas en Vagrant, una para el servidor de Apache y otra para MySQL.
#### [Vagrantfile de las dos máquinas.](#vagrantfile-de-las-dos-máquinas)
 ![](Img/vagrantfile.png)

### Creamos un par de scripts de aprovisionamiento para facilitar la configuración de las máquinas.

#### [Script para el servidor Apache.](#script-para-el-servidor-apache)
 ![](Img/scriptApache.png)

#### [Script para el servidor MySQL.](#script-para-el-servidor-mysql)
 ![](Img/scriptSql.png)
<br />
<br />
<br />

## **2. Configuración servidor MySQL.**
 <br />
<br />

### [Clonamos la carpeta de GitHub en nuestra máquina SQL.](#clonar-la-carpeta-de-github-en-nuestra-máquina-sql)
![](Img/gitclone.png)
### [Nos dirigimos al directorio */etc/mysql/mariadb.conf.d* y modificamos el fichero *50-server.cnf*, cambiamos la *bind-address* y ponemos la IP de nuestra máquina.](#nos-dirigimos-al-directorio-etcmysqlmariadbconfd-y-modificamos-el-fichero-50-servercnf-cambiamos-la-bind-address-y-ponemos-la-ip-de-nuestra-máquina)
![](Img/scriptSql2.png)
### [Ejecutamos el Script SQL en nuestro servidor.](#ejecutamos-el-script-sql-en-nuestro-servidor)
![](Img/confSQL.png)
### [Después creamos un usuario de MySQL pero con la IP de nuestro servidor Apache.](#después-creamos-un-usuario-de-mysql-pero-con-la-ip-de-nuestro-servidor-apache)
![](Img/user1.png)
<br />
<br />
<br />
<br />
<br />
<br />

## **3. Configuración servidor Apache.**
<br />
<br />

### [Nos dirigimos al directorio */var/www*, movemos los archivos src de la carpeta de GitHub.](#nos-dirigimos-al-directorio-varwww-movemos-los-archivos-src-de-la-carpeta-de-github)
![](Img/indexphp.png)

### [Ahora nos vamos a la carpeta de sites-available en */etc/apache2/sites-available* y creamos un fichero de configuración.](#ahora-nos-vamos-a-la-carpeta-de-sites-available-en-etcapache2sites-available-y-creamos-un-fichero-de-configuración)
![](Img/archivoconf.png)

### [Editamos el fichero de configuración y ponemos la ruta de la carpeta que hemos creado anteriormente.](#editamos-el-fichero-de-configuración-y-ponemos-la-ruta-de-la-carpeta-que-hemos-creado-anteriormente)
![](Img/confapache.png)

### [A continuación habilitamos el fichero de configuración que hemos creado con a2ensite.](#a-continuación-habilitamos-el-fichero-de-configuración-que-hemos-creado-con-a2ensite)
![](Img/habilitarconf.png)

### [Ahora nos dirigimos a */etc/apache2/sites-enabled* y desactivamos el fichero de configuración anterior con **a2dissite**. Después de esto, recargamos el Apache2 con **sudo systemctl reload apache2**.](#ahora-nos-dirigimos-a-etcapache2sites-enabled-y-desactivamos-el-fichero-de-configuración-anterior-con-a2dissite-después-de-esto-recargamos-el-apache2-con-sudo-systemctl-reload-apache2)
![](Img/deshabilitarconf.png)

### [Lo siguiente es entrar en la carpeta creada en */var/www* y editar el fichero config.php, donde pone localhost, ponemos la IP de la máquina de MySQL y cambiamos los datos de usuario y contraseña.](#lo-siguiente-es-entrar-en-la-carpeta-creada-en-varwww-y-editar-el-fichero-configphp-donde-pone-localhost-ponemos-la-ip-de-la-máquina-de-mysql-y-cambiamos-los-datos-de-usuario-y-contraseña)
![](Img/phpconf.png)

### [Ahora en el servidor Apache, ingresamos al servidor MySQL con el siguiente comando: **mysql -u nombreusuario -p -h ipmysql**.](#ahora-en-el-servidor-apache-ingresamos-al-servidor-mysql-con-el-siguiente-comando-mysql-u-nombreusuario-p-h-ipmysql)
![](Img/comprobacion.png)

### [Ahora, si ponemos la dirección de la máquina de Apache en Google, veremos la página del LAMP.](#ahora-si-ponemos-la-dirección-de-la-máquina-de-apache-en-google-veremos-la-página-del-lamp)
![](Img/resultado.png)