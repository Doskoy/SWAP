# Practica 4 SWAP   

### Asegurar la granja Web

###### Autores: Antonio Carrasco Castro, Fernado Roldán Zafra  

## Objetivos 
I. Instalar un certificado SSL para configurar el acceso HTTPS a los servidores  
II. Configurar las reglas del cortafuegos para proteger la granja web  

## -Sesión 4  

### Objetivo I Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.
Vamos a proceder a instalar el certificado en la maquina 1, el procedimiento es el siguiente:

-Introducimos la siguiente secuencia de ordenes:
	a2enmod ssl
	service apache2 restart
	mkdir /etc/apache2/ssl
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt

-En este punto nos pedira que introduzcamos alguna información: 
 
![img](https://github.com/Doskoy/SWAP/tree/master/Practica4/img/Captura1.png)  

-Modificamos el archivo /etc/apache2/sites-avaliable/default-ssl.conf añadiendole las 2 lineas que se especifican en el guion de la práctica.

![img](https://github.com/Doskoy/SWAP/tree/master/Practica4/img/Captura2.png)  

-Para comprobar que el certificado se ha instalado correctamente nos conectamos mediante curl al servidor utilizando el https tal y como se ve a continuación: 

![img](https://github.com/Doskoy/SWAP/tree/master/Practica4/img/Captura6.png)  

Como se puede ver nos da un error, por lo que debemos utilizar la opción -k para poder conectarnos. Esto significa que funciona conrrectamente.

-Copiamos las claves en el balanceador con el siguiente comando:

rsync -avz -e ssh <ip_maquina_configurada>:/etc/apache2/ssl /etc/apache2/ssl

![img](https://github.com/Doskoy/SWAP/tree/master/Practica4/img/Captura3.png)  


### Objetivo II Configurar las reglas del cortafuegos para proteger la granja web

Para configurar el cortafuegos existen muchas tipos de configuraciones, yo he optado por seguir la del guión de practicas con algunas modificaciones. Para ello hay que crear un script y hacer que se ejecute cada vez que se inicie el sistema. Esta configuracion solo se ha realizado en la maquina1.

El script usado es el siguiente:

![img](https://github.com/Doskoy/SWAP/tree/master/Practica3/img/Captura4.png)  

Para hacer que se ejecute cada vez que se inicie el sistema añadimos al crontab la siguiente linea: 

![img](https://github.com/Doskoy/SWAP/tree/master/Practica3/img/Captura5.png)  
