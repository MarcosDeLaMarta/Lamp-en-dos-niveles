# **Lamp-en-dos-niveles**
<br />
<br />

## **1. Creación y configuracion de las maquinas.**
<br />
<br />

### Creamos dos maquina en Vagrant una para el servidor de Apache y otra para el Mysql
#### Vagrantfile de las dos maquinas.
 ![](Img/vagrantfile.png)

### Creamos un par de scripts de aprovisionamientopara facilitar la configuracion de las maquinas.

#### Script para el servidor Apache.
 ![](Img/scripApache.png)

#### Script para servidor SQL.
 ![](Img/scriptSql.png)
<br />
<br />
<br />

## **2. Configuracion servidor SQL.**
 <br />
<br />

### Clonamos la carpeta de github a nuestra maquina sql
![](Img/gitclone.png)
### Nos vamos directorio */etc/mysql/mariadb.conf.d* y modificamos el fichero *50-server.cnf* cambiamos la *bind-address* y ponemos la ip de nuestra maquina.
![](Img/scriptSql2.png)
### Ejecutamos el Script sql en nuestro servidor.
![](Img/confSQL.png)
### Despues creamos un usuario mysql pero con la ip de nuestro servidor apache.
![](Img/user1.png)
<br />
<br />
<br />
<br />
<br />
<br />

## **3. Configuracion servidor Apache.**
<br />
<br />

### Nos dirigimos al directorio */var/www* movemos los archivos src de la carpeta de github.
![](Img/indexphp.png)

### Ahora nos vamos a la carpeta de sites-available en */etc/apache2/sites-availables* y creamos un fichero de configuración.
![](Img/archivoconf.png)

### Editamos el fichero de configuración y ponemos la ruta de la carpeta que hemos craddo anteriormente

![](Img/confapache.png)

### Acontinuación habilitamos el fichero de configuración que hemos creado con a2ensite.
![](Img/habilitarconf.png)

### ### Ahora nos vamos a */etc/apache2/sites-enabled* y desactivamos el fichero de configuración anterior con **a2dissite**. Despues de esto recargamos el apache2 con **sudo systemctl reload apache2**.
![](Img/deshabilitarconf.png)

### Lo siguiente es entrar en la carpeta creada en */var/www* y editar el fichero config.php y donde pone localhost ponemos la ip de la maquina de sql y cambiamos los datos de user y password.
![](Img/phpconf.png)

### Ahora en el servidor apache entramos a servidor mysql con el siguiente comando **mysql -u nombreusuario -p -h ipmysql**.
![](Img/phpconf.png)