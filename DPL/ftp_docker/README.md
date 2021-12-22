Daniel de Jesús Álvarez Miranda		2º DAW


# Instalación y Administración de Servidores de Transferencia de Archivos.




## Indice

[Imagen Docker](#item1)

[Imagen ATMOZ](#item2)

[Verificación](#item3)

[Configuración](#item4)



<a name = "item1"></a>

## Imagen Docker

Lo primero que debemos hacer es buscar la imagen sftp en los repositorios de docker. Para ello, pondremos lo siguiente:

```console
sudo docker search sftp
```

![](img/01.png)

<a name = "item2"></a>

## Imagen ATMOZ

Utilizaremos la imagen desarrollada por atmoz sobre sftp. Lanzamos el siguiente comando:

```console
sudo docker run --name mysftp -p 2294:22 -d atmoz/sftp admin:admin:::upload
```

![](img/02.png)


<a name = "item3"></a>

## Verificación

Verificamos que se ha descargado y funcione correctamente.

```console
sudo docker ps | grep sftp
```

![](img/03.png)

Como acabamos de ver, la imagen ha sido descargada correctamente. Ahora procederemos a probar su funcionamiento.

```console
sudo docker inspect ffa078007f2e | grep "IPAddress"
```

![](img/04.png)


<a name = "item4"></a>

## Configuración

Configuramos el directorio home de SFTP.

```console
sudo  docker run --name mysftp2 -v /host/upload:/home/admin/upload --privileged=true -p 2295:22 -d atmoz/sftp admin:admin:1001
```

![](img/05.png)

