Daniel de Jesús Álvarez Miranda		2º DAW


# Instalación de servicios REST/WS Wildfly


## Indice

[Instalación de Servicio Hello-RS](#item1)

[Instalación de Servicio Hello-WS](#item2)


## Instalación de Servicio Hello-RS

Accedemos al directorio “helloworld-rs” y ejecutamos el siguiente comando:

```console
mvn clean install
```

![](img/01.png)


Una vez terminado, vamos a la pestaña “deployments” y pulsamos sobre el “+”. Seleccionamos la carpeta donde se encuentra el proyecto helloworld-rs y buscamos el archivo con la extensión .war.

![](img/02.png)

![](img/03.png)

Para verificar que todo está correctamente, vamos a nuestro navegador y en la URL ponemos la dirección del servidor. En nuestro caso, pondremos localhost y conectamos por el puerto 8083 y “/helloworld-rs/”.

![](img/04.png)


## Instalación de Servicio Hello-WS

Accedemos al directorio “helloworld-ws” y ejecutamos el siguiente comando:

```console
mvn clean install
```

![](img/05.png)


Una vez terminado, vamos a la pestaña “deployments” y pulsamos sobre el “+”. Seleccionamos la carpeta donde se encuentra el proyecto helloworld-ws y buscamos el archivo con la extensión .war.

![](img/06.png)

Para verificar que todo está correctamente, vamos a nuestro navegador y en la URL ponemos la dirección del servidor. En nuestro caso, pondremos localhost y conectamos por el puerto 8083 y “/helloworld-ws/”.

![](img/07.png)
