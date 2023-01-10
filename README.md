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

# 5.- Referencias.
- [https://es.wikipedia.org/wiki/Nginx](https://es.wikipedia.org/wiki/Nginx)

- [https://marketersgroup.es/diferencias-entre-apache-y-nginx/#:~:text=El%20servidor%20de%20Apache%20tiene,velocidad%20y%20mejora%20el%20rendimiento.](https://marketersgroup.es/diferencias-entre-apache-y-nginx/#:~:text=El%20servidor%20de%20Apache%20tiene,velocidad%20y%20mejora%20el%20rendimiento.)

- [https://www.javatpoint.com/difference-between-apache-and-nginx](https://www.javatpoint.com/difference-between-apache-and-nginx)
