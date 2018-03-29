# Practica 1 SWAP   

### Preparación de las herramientas

###### Autores: Antonio Carrasco Castro, Fernado Roldán Zafra  

## Objetivos 
I. Acceder por ssh de una máquina a otra  
II. Acceder mediante la herramienta curl desde una máquina a la otra  

## -Pasos previos  
* **(Instalación de software y máquinas)**  
Para el comienzo de este apartado, instalaremos el software VMware con el que se instalarán dos máquinas virtuales (en este caso ubuntu server 16.04.4 LTS). Necesitaremos el paquete openSSH y LAMP que como se explica en el guión se puede instalar durante la instalación. Si no se instala ningún paquete se puede hacer mediante linea de comandos una vez instalado con: 
	
	Para el paquete openSHH:  
**sudo apt-get install openssh-server openssh-client**
	
	Para el paquete LAMP:  
 **sudo apt-get install apache2**  
 **sudo apt-get install mysql-server mysql-client**  
**sudo apt-get install php7.0-mysql php7.0-curl php7.0-json php7.0-cgi  php7.0 libapache2-mod-php7**  

Dejo un posible tutorial facilitado en el guión a seguir:

[Referencia instalar LAMP](https://www.unixmen.com/how-to-install-lamp-stack-on-ubuntu-16-04/)  

## -Sesión 1  
Una vez instalado procedemos al objetivo uno, conexión SSH:

### Nota ###  
Levantar ssh-> sudo /etc/init.d/ssh start  
Conectarse-> ssh user@ipUser  

![img](https://github.com/jonio1992/SWAP/blob/master/practica1/img/1.png)  
Levantando el servicio ssh de la maquina swap1 y visualizando su ip.

![img](https://github.com/jonio1992/SWAP/blob/master/practica1/img/2.png)  
Levantando el servicio ssh de la maquina swap2 y visualizando su ip.

![img](https://github.com/jonio1992/SWAP/blob/master/practica1/img/3.png)  
Conectándonos desde el PC anfitrión a las maquinas mediante el protocolo SSH.

Para el objetivo dos se va a generar un archivo .html el cual se pondrá en el directorio var/www/sesion1.  
Procedemos a ver las direcciones ip de cada máquina.  

![img](https://github.com/jonio1992/SWAP/blob/master/practica1/img/4.png)  

Y ahora vamos a hacer una petición a cada máquina con la opción curl.  
![img](https://github.com/jonio1992/SWAP/blob/master/practica1/img/5.png)  

Como se ve en la imagen, se puede acceder de la máquina SWAP1 al documento contenido en SWAP2 y viceversa. Adicionalmente desde la máquina anfitrión se ha hecho la petición para comprobar la conexión de todas las máquinas.  
