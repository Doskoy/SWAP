# Practica 1 SWAP   

### Preparación de las herramientas

###### Autores: Antonio Carrasco Castro, Fernado Roldán Zafra  

## Objetivos 
I. Copiar archivos mediante ssh  
II. Clonar contenido entre máquinas	

III. Configurar ssh para acceder a máquinas remotas sin contraseña
	
IV. Establecer tareas en cron 	

## -Pasos previos  
* **(Instalación de software y máquinas)**  
Para el realizar esta práctica se han utilizado las máquinas virtuales que se crearon para la realización de la práctica anterior. Ademas de esto, es necesario instalar la herramienta rsync utilizando el siguiente comando:	

**sudo apt-get install rsync**
 
Para copiar ficheros o directamente crearlos en un equipo remoto, podemos utilizar varios metodos:

1.- Redirigir la salida de stdout con un pipeline hacia el ssh.

### Nota ###  
Este metodo sirve como algo puntual, pero en el caso de que queramos sincronizar grandes cantidades de datos tendremos que utilizar el metodo descrito mas abajo.

![img](https://github.com/Doskoy/SWAP/blob/master/Practica2/img/1.PNG)  
Creando un .tar en un equipo remoto utilizando ssh.

2.-Utilizar la herramienta rsync.
Para clonar en la maquina 2 el contenido de una carpeta concreta de la maquina 1 utilizaremos el siguiente comando: 

**rsync -avz -e ssh ubuntu1@192.168.125.128:/var/www /var/www**

![img](https://github.com/Doskoy/SWAP/blob/master/Practica2/img/2.PNG)  
Clonando la carpeta /var/www de la maquina 1 en la maquina 2 

En el caso de que queramos copiar un directorio en concreto e ignorar otros utilizaremos el siguiente comando: 

**rsync -avz --delete --exclude=**/stats --exclude=**/error
exclude=**/files/pictures -e ssh maquina1:/var/www/ /var/www/**

En este caso estamos haciendo la copia del directorio /var/www pero ignorando /var/www/error, /var/www/stats y /var/www/files/pictures

![img](https://github.com/Doskoy/SWAP/blob/master/Practica2/img/3.PNG)   

Como vemos cada vez que accedemos de una maquina a la otra debemos de introducir la contraseña, y en el caso de que, por ejemplo, queramos defenir una tarea automatica, no podriamos estar constantemente escribiendo la contraseña. Por lo que parece lógico hacer que esta no se pida cada vez. 

Para ello vamos a generar las claves pública y privada. Para ello utilizamos el siguiente comando: 
**ssh-keygen -b 4096 -t rsa**

Una vez generada la clave en la maquina secundaria utilizamos el comando ssh-copy-id para copiarla en la lista de claves autorizadas de la maquina principal: 
**ssh-copy-id ubuntu1@192.168.125.128**
![img](https://github.com/Doskoy/SWAP/blob/master/Practica2/img/4.PNG)  

Una vez hecho esto, la maquina secundaria ya puede conectarse a la principal sin introducir la contraseña

![img](https://github.com/Doskoy/SWAP/blob/master/Practica2/img/5.PNG)


Para programar tareas modificaremos el fichero /etc/crontab el cual es utilizado por el proceso cron que lo revisa cada minuto para ver si tiene que ejecutar algun comando. 

En este caso se va a establecer una tarea que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas

Para ello se ha añadido la linea que se puede ver en la siguiente captura al fichero /etc/crontab.

![img](https://github.com/Doskoy/SWAP/blob/master/Practica2/img/6.PNG)
