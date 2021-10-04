Daniel de Jesús Álvarez Miranda		2º DAW


# Instalación de GitLab en Linux


## Indice

[Actualización de los repositorios](#item1)

[Paquetes adicionales](#item2)

[Instalación de GitLab](#item3)

[Acceso](#item4)


<a name = "item1"></a>
## Actualización de los repositorios
---

Antes de empezar, debemos descargar las actualizaciones pendientes y actualizar.

![](img/01.png)


<a name = "item2"></a>
## Paquetes adicionales
---

Se necesitarán paquetes adicionales para instalar GitLab en Ubuntu.

![](img/02.png)


<a name = "item3"></a>
## Instalación de GitLab
---

Descargamos e instalamos Gitlab con los siguientes comandos.

```console

curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash

```

![](img/03.png)

```console

sudo apt install gitlab-ce

```

![](img/04.png)

Hasta que nos aparece el siguiente mensaje:

![](img/05.png)

Para finalizar, lanzamos el siguiente comando para configurarlo.

```console

sudo gitlab-ctl reconfigure

```

![](img/06.png)



El final sería algo así.

![](img/07.png)


<a name = "item4"></a>
## Acceso
---

Debemos ir al navegador y poner nuestra IP o localhost en la URL.

![](img/08.png)


Una vez logueados, veremos esta pantalla.

![](img/09.png)
