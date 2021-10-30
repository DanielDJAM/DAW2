Daniel de Jesús Álvarez Miranda		2º DAW


# PHP en Apache y Nginx


## Indice

[PHP para Apache](#item1)

[PHP para Nginx](#item2)

[Comprobar PHP en Ubuntu](#item3)


<a name = "item1"></a>

## PHP para Apache

Si queremos usar el PHP para Apache, necesitaremos el paquete libapache2-mod-php. Para ello, lanzaremos el siguiente comando:

```console
sudo apt install -y php
```

![](img/01.png)


<a name = "item2"></a>

## PHP para Nginx

En caso de querer usar PHP en Nginx, necesitaremos el paquere php-fpm. Podemos instalarlo del siguiente modo:

```console
sudo apt install -y php-fpm
```


![](img/02.png)


Luego será necesario configurar Nginx para que conecte con el servicio PHP-FPM, editando su archivo de configuración:

```console

sudo nano /etc/nginx/sites-available/default

```

![](img/03.png)

Buscamos y activamos la configuración adecuada, en nuestro caso correspondiente a PHP-FPM.

```console

...

# pass PHP scripts to FastCGI server

#

location ~ \.php$ {

    include snippets/fastcgi-php.conf;

#

#       # With php-fpm (or other unix sockets):

    fastcgi\_pass unix:/var/run/php/php7.4-fpm.sock;

#       # With php-cgi (or other tcp sockets):

#       fastcgi\_pass 127.0.0.1:9000;

}

...

```

![](img/04.png)



Una vez terminado de configurar el archivo, debemos recargar el servicio de Nginx para que los cambios surtan efecto.

```console
sudo systemctl reload nginx
```

![](img/05.png)


<a name = "item3"></a>

## Comprobar PHP en Ubuntu

Para comprobar que está todo correctamente, necesitamos crear un archivo php y verlo a través del navegador.

```console
sudo nano /var/www/html/info.php
```

```console
<?php phpinfo();
```

![](img/06.png)


Luego vamos al navegador y con la ruta: IP/info.php nos tendría que salir una página como la siguiente.

![](img/07.png)