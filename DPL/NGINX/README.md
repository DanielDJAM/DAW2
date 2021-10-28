Daniel de Jesús Álvarez Miranda		2º DAW


# Instalar Nginx en Linux


## Indice

[Instalar Nginx.](#item1)

[Configurar Firewall](#item2)

[Comprobar el servidor web.](#item3)

[Configurar bloques de servidor](#item4)

[EXTRA](#item5)


<a name = "item1"></a>

## Instalar Nginx.

Aprovechando que Nginx está disponibles en los repositorios de Ubuntu, vamos a descargarlo con el comando:

```console

sudo apt install nginx

```

![](img/01.png)

<a name = "item2"></a>

## Configurar Firewall

Para que funcione nuestro Nginx, debemos habilitar el acceso al servicio. Con el siguiente comando podremos listar los diferentes perfiles.

```console

sudo ufw app list

```

![](img/02.png)


Habilitamos la regla “Nginx HTTP” del siguiente modo y comprobamos:

```console

sudo ufw allow 'Nginx HTTP'

```

![](img/03.png)

![](img/04.png)

<a name = "item3"></a>

## Comprobar el servidor web.

Después de permitir el acceso del Firewall al servicio, comprobamos el estado de Nginx.

```console

systemctl status nginx

```

![](img/05.png)

Podemos observar que el servicio está activo pero para comprobarlo definitivamente, buscamos en nuestro navegador http://localhost:80. Si no nos sale nada, quizás tengamos un problema de puertos y debamos resolverlo. Podremos ver información más detallada en “/var/log/nginx/error.log”

Si queremos saber la ip de nuestra máquina o el de un servidor en la nube, debemos lanzar el siguiente comando:

```console

curl -4 icanhazip.com

```

![](img/06.png)

Cuando obtenga la IP, introdúzcala en el navegador del siguiente modo:

```console

http://your_server_ip:puerto

```

![](img/07.png)

<a name = "item4"></a>

## Configurar bloques de servidor

Creamos el directorio para your_domain usando el indicador -p para crear cualquier directorio principal necesario.

```console

sudo mkdir -p /var/www/your_domain/html

```

![](img/08.png)

Seguidamente,  asignamos la propiedad del directorio con la variable de entorno $USER.

```console

sudo chown -R $USER:$USER /var/www/your_domain/html

```

![](img/09.png)

![](img/10.png)


Cambiamos los permisos recursivamente de todo lo que contenga el directorio your_domain.

```console

sudo chmod -R 755 /var/www/your_domain

```

![](img/11.png)

Luego creamos con un editor de texto un index.html. (En la imagen sale “/var/www/your_domain/html/index.html”. Esto es un error, se debe eliminar del archivo).

```console

nano /var/www/your_domain/html/index.html

```

```console

 <html>

    <head>

      <title>Welcome to your_domain!</title>

    </head>

    <body>

    <h1>Success!  The your_domain server block is working!</h1>

  </body>

</html>

```

![](img/12.png)


Para que lo escrito anteriormente pueda mostrarse en el navegador, debemos crear un bloque de servidor con las directivas correctas.

```console

sudo nano /etc/nginx/sites-available/your_domain

```

```console

 server {

      listen 80;

      listen [::]:80;

      root /var/www/your_domain/html;

      index index.html index.htm index.nginx-debian.html;

      server_name your_domain www.your_domain;

      location / {

      try_files $uri $uri/ =404;

    }

}

```

![](img/13.png)

Habilitamos el archivo creando un enlace simbólico entre él y el directorio sites-enabled.

```console

sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/

```

![](img/14.png)

![](img/15.png)

Para evitar un problema de memoria de depósito de hash que pueda surgir al agregar nombres de servidor, es necesario aplicar ajustes a un valor en el archivo “/etc/nginx/nginx.conf ”.

Encuentre la directiva server_names_hash_bucket_size y borre el símbolo # para eliminar el comentario de la línea. Si utiliza nano, presione CTRL y w para buscar rápidamente palabras en el archivo.

```console

sudo nano /etc/nginx/nginx.conf

```

```console

http {

...

    server_names_hash_bucket_size 64;

...

}

…

```

![](img/16.png)


![](img/17.png)


Para asegurarnos que no tenemos ningún error de sintaxis en los archivos que hemos creado/modificado, usaremos el siguiente comando para comprobar que todo está correctamente.

```console

sudo nginx -t

```

![](img/18.png)

Por último, reiniciamos el servicio de Nginx para que los cambios surtan efecto.

```console

sudo systemctl restart nginx

```

![](img/19.png)

<a name = "item5"></a>

## EXTRA

Si no nos arranca habiendo hecho todo lo anterior, debemos ver que en nuestro archivo “/etc/hosts” esté la IP y el nombre de nuestra página.

![](img/20.png)


Este es el resultado.

![](img/21.png)
