Daniel de Jesús Álvarez Miranda		2º DAW

# Instalación de Apache-Tomcat en Linux

# 1. Instalación

## 1.1 Descarga.

Descargamos un archivo tar.gz con el comando wget desde la página oficial.

```console

wget https://downloads.apache.org/tomcat/tomcat-10/v10.0.12/bin/apache-tomcat-10.0.12.tar.gz

```

![](img/01.png)

## 1.2 Crear usuario.

Creamos el usuario tomcat.

```console

sudo useradd -U -m -d /opt/tomcat -k /dev/null -s /bin/false tomcat

```

![](img/02.png)

## 1.3 Descomprimir archivos.

Descomprimimos el archivo tar con el siguiente comando.

```console

sudo tar xvf apache-tomcat-10.0.12.tar.gz -C /opt/tomcat/

```

![](img/03.png)

## 1.4 Cambiar permisos.

Cambiamos los permisos de “/opt/tomcat” y podemos como dueño a tomcat.

```console

sudo chown -R tomcat: /opt/tomcat/

```

![](img/04.png)



## 1.5 Enlace simbólico.

Creamos un enlace simbólico desde “/opt/tomcat/apache-tomcat-10.0.12/” hasta “/opt/tomcat/apache-tomcat”.

```console
sudo ln -s /opt/tomcat/apache-tomcat-10.0.12/ /opt/tomcat/apache-tomcat
```

![](img/05.png)

## 1.6 Configuración Tomcat.

Configuramos tomcat. Para ello creamos un fichero de texto en la ruta “/etc/systemd/system/” con el nombre de “tomcat10.service” y dentro de éste contendrá lo siguiente:

```console

sudo nano /etc/systemd/system/tomcat10.service

```

```console

[Unit]

Description=Tomcat 10.0 servlet container para Ubuntu 20.04 LTS

After=network.target

[Service]

Type=forking

User=tomcat

Group=tomcat

Environment="JAVA\_OPTS=-Djava.security.egd=file:///dev/urandom"

Environment="CATALINA\_BASE=/opt/tomcat/apache-tomcat"

Environment="CATALINA\_HOME=/opt/tomcat/apache-tomcat"

Environment="CATALINA\_PID=/opt/tomcat/apache-tomcat/temp/tomcat.pid"

Environment="CATALINA\_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

ExecStart=/opt/tomcat/apache-tomcat/bin/startup.sh

ExecStop=/opt/tomcat/apache-tomcat/bin/shutdown.sh

[Install]

WantedBy=multi-user.target

```

![](img/06.png)


## 1.7 Iniciar servicio.

Iniciamos el servicio con el nombre que le dimos anteriormente.

```console

sudo systemctl start tomcat10

```

![](img/07.png)

## 1.8 Estado del servicio.

Consultamos el estado de nuestro servicio con el siguiente comando. Debe de estar en modo activo.

```console

sudo systemctl status tomcat10

```

![](img/08.png)



## 1.9 Arranque automático.

Si queremos que con cada arranque se inicie el servicio, debemos escribir lo siguiente:

```console

sudo systemctl enable tomcat10

```

![](img/09.png)

# Acceso a Tomcat

Para acceder, debemos de poner localhost y el puerto 8080.

![](img/10.png)
