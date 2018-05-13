# Practica 3 SWAP   

### Balanceo de carga

###### Autores: Antonio Carrasco Castro, Fernado Roldán Zafra  

## Objetivos 
I. Configurar una máquina e instalar el nginx como balanceador de carga.  
II. Configurar una máquina e instalar el haproxy como balanceador de carga.  

## Preparativos
En primer lugar para realizar mas facilmente esta practica vamos a eliminar del crontab la rutina rsync que se encuentra activa debido a la practica anterior. Tambien se ha usado la herramienta nmap para ver los puertos ocupados. Utilizando el siguiente comando:

sudo nmap -sT -O localhost


## -Sesión 3  


### Nota 
Levantar ssh -> sudo /etc/init.d/ssh start  
Conectarse -> ssh user@ipUser  
Acciones balanceador  -> /etc/init.d/{haproxy, nginx} {start, status, stop}  

### Objetivo I Configurar una máquina e instalar el nginx como balanceador de carga.
Para esta práctica he creado una nueva maquina que hará de balanceador de carga hacia las otras dos máquinas usadas en las anteriores prácticas (SWAP1 y SWAP2).  

Para la instalción de nginx, se han usado los comandos que se comentan en el guion de prácticas 3:  

sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove  

sudo apt-get install nginx  

/etc/init.d/nginx start  

Pasamos a la configuración de nginx. Una configuración básica sobre el archivo alojado en:   /etc/nginx/conf.d/default.conf  
 
![img](https://github.com/Doskoy/SWAP/tree/master/Practica3/img/Captura1.png)  

En esta imagen se muestra las ip de las máquinas servidoras y la configuración para la máquina que hará de balaceador de carga.

Como se puede ver, el balanceador funciona correctamente:
![img](https://github.com/Doskoy/SWAP/tree/master/Practica3/img/Captura2.png)  


### Objetivo II Configurar una máquina e instalar el haproxy como balanceador de carga.

Para la instalción de haproxy, se han usado los comandos que se comentan en el guion de prácticas 3:  

* sudo apt-get install haproxy  
* sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg  

Una vez instalado el programa haproxy en la máquina que va a balancear, nos vamos a su archivo de configuración alojado en: /etc/haproxy/haproxy.cfg.  

![img](https://github.com/Doskoy/SWAP/tree/master/Practica3/img/Captura3.png)  

Se puede ver que el servicio esta activo y que balancea la carga correctamente:

![img](https://github.com/Doskoy/SWAP/tree/master/Practica3/img/Captura4.png)  

![img](https://github.com/Doskoy/SWAP/tree/master/Practica3/img/Captura5.png)  