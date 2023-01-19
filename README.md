# 1.-Introducción.
Nginx es un servidor web que también se puede utilizar como proxy inverso, equilibrador de carga, proxy de correo y caché HTTP.

# 2.-Comparativa con Apache.
![](imagenes/Captura.PNG)

# 3.- Instalación.
![](imagenes/instalacion.PNG)

# 4.- Casos prácticos.
## a) Versión de Nginx instalado.
![](imagenes/version.PNG)

## b) Ficheros de configuración.
Los ficheros de configuración se encuentran en `/etc/nginx`
![](imagenes/configuracion.PNG)

El fichero de configuración por defecto es `/etc/nginx/sites-enabled/default` 
![](imagenes/confdefault.PNG)


## c) Página web por defecto:
La página web por defecto se encuentra en `/var/www/html` 
![](imagenes/index.PNG)

Se puede acceder con el navegador.
![](imagenes/paginapordefecto.PNG)

Creamos un index.html
![](imagenes/personalizada.PNG)

## d) Virtual Hosting:
Queremos que nuestro servidor web ofrezca balanceo de carga desde https  a dos sitios web que tengan también https.

Primero, configuramos en dos maquinas virtuales la ip estática (.171, .172) y cambiamos la página web por defecto.
![](imagenes/servidor1index.PNG)
![](imagenes/servidor2index.PNG)

En una tercera máquina virtual (con ip .170) vamos a configurar el balanceador, que gestionará las peticiones y decidirá que servidor responde.

En la máquina balanceador, hacemos una copia del fichero de configuración por defecto y creamos otro dentro de `/etc/nginx/conf.d/` llamado load-balancing.conf.
![](imagenes/cambiarConfDefecto.PNG)
![](imagenes/configuracionBalanceador.PNG)

Comprobamos que la sintaxis es correcta mediante `nginx -t` y reiniciamos el servicio.

Creamos una máquina cliente, y modificamos su `/etc/hosts` añadiendo la ip del balanceador de cargo y su dominio.
 ![](imagenes/hostCliente.PNG)

 Para finalizar, entramos al navegador y escribimos la dirección de enlace y vemos como el balanceador de carga se encarga de redistribuir las peticiones entre el servidor 1 y el 2.
 ![](imagenes/comprobacionServidor1.PNG)
![](imagenes/comprobacionServidor2.PNG)

### Configurar https
Para configurar https hacen falta dos cosas:
1. Escuchar en el puerto 443 y usar ssl en la directiva listen.
2. Crear un certificado e indicar la ruta en la configuración de nginx.

Generamos el certificado del balanceador con el siguiente comando:

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/antonioBalanceador.key -out /etc/ssl/certs/antonioBalanceador.crt
```

 ![](imagenes/crearCertificado.PNG)

 Modificamos la configuración de nginx de la siguiente manera:

 ![](imagenes/configuracionSSL.PNG)


Generamos el certificado de los servidores (los siguientes pasos hay que hacerlo tanto en el servidor 1 como en el 2):
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/antonioServidor.key -out /etc/ssl/certs/antonioServidor.crt
```

Modificamos la configuración de nginx de la siguiente manera:
 ![](imagenes/configuracionSSLservidor.PNG)

Podemos comprobar en el navegador que el balanceador redirecciona y responde con https
 ![](imagenes/balanceadorNavegador.PNG)












# 5.- Referencias.
- [https://es.wikipedia.org/wiki/Nginx](https://es.wikipedia.org/wiki/Nginx)

- [https://marketersgroup.es/diferencias-entre-apache-y-nginx/#:~:text=El%20servidor%20de%20Apache%20tiene,velocidad%20y%20mejora%20el%20rendimiento.](https://marketersgroup.es/diferencias-entre-apache-y-nginx/#:~:text=El%20servidor%20de%20Apache%20tiene,velocidad%20y%20mejora%20el%20rendimiento.)

- [https://www.javatpoint.com/difference-between-apache-and-nginx](https://www.javatpoint.com/difference-between-apache-and-nginx)

- [https://nginx.org/en/docs/http/configuring_https_servers.html](https://nginx.org/en/docs/http/configuring_https_servers.html)

- [https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-on-centos-7](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-on-centos-7)