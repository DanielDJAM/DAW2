Daniel de Jesús Álvarez Miranda		DAW – 2º


# Manipulación avanzada de repositorios en Git

---

##  INDICE

[Previo](#previo)

[Ejercicio 1](#item1)

[Ejercicio 2](#item2)

[Ejercicio 3](#item3)

[Ejercicio 4](#item4)

[Ejercicio 5](#item5)

[Ejercicio 6](#item6)

[Ejercicio 7](#item7)

[Ejercicio 8](#item8)

<a name = "previo"></a>

# **Previo**

Clonamos el repositorio del profesor y nos situamos en la ruta de libro.

```console
git clone https://github.com/jpexposito/libro.git
cd libro
```

![](img/01.png)

<a name = "item1"></a>
# **Ejercicio 1**

Mostramos el historial de cambios en el repositorio, creamos el directorio capítulos y dentro de ella, el fichero capítulo1.txt. Luego añadimos los cambios temporales, hacemos el commit y volvemos a mostrar el historial.

```console
git log
mkdir capitulos
nano capitulos/capitulo1.txt
Git es un sistema de control de versiones ideado por Linus Torvalds.
git add *
git commit -m "Añadido capítulo 1."
git log
```

![](img/02.png)
![](img/03.png)
![](img/04.png)

<a name = "item2"></a>
# **Ejercicio 2**

Creamos el fichero capitulo2.txt con lo siguiente:

```console
El flujo de trabajo básico con Git consiste en: 1- Hacer cambios en el repositorio. 2- Añadir los cambios a la zona de intercambio temporal. 3- Hacer un commit de los cambios.
```

![](img/05.png)

Añadimos los cambios a la zona temporal, hacemos el commit y miramos los cambios entre la última versión y hace dos versiones.

![](img/06.png)

<a name = "item3"></a>
# **Ejercicio 3**
---
Creamos el fichero capitulo3.txt y añadimos el siguiente texto:

```console
Git permite la creación de ramas lo que permite tener distintas versiones del mismo proyecto y trabajar de manera simultanea en ellas.
```

Añadimos los cambios a la zona temporal, realizamos el commit y miramos las diferencias entre la última y la primera verisón.

![](img/07.png)

![](img/08.png)

<a name = "item4"></a>
# **Ejercicio 4**
---
A partir de aquí, el profesor actualizó su repositorio y algunas cosas no cuadran.

Creamos el fichero indice.txt y añadimos la siguiente línea:

```console
Indice de los cápitulos, con conceptos avanzados de git.
```

![](img/09.png)

Añadimos los cambios a la zona temporal, realizamos el commit y miramos quien ha hecho cambios en dicho fichero.

![](img/10.png)

<a name = "item5"></a>
# **Ejercicio 5**
---
Creamos una nueva rama y mostramos las ramas.
# ![](img/11.png)

<a name = "item6"></a>
# **Ejercicio 6**
---
Cambiamos a la nueva rama, creamos el fichero bibliografia.txt y añadimos el siguiente texto:

```console
Chacon, S. and Straub, B. Pro Git. Apress.
```

Añadimos los cambios a la zona temporal, realizamos el commit y mostramos la historia del repositorio incluyendo todas las ramas.

![](img/12.png)

![](img/13.png)

<a name = "item7"></a>
# **Ejercicio 7**
---
Volvemos a cambiar a la rama principal y creamos el mismo fichero que el anterior, esta vez con un poco más de texto:

```console
Chacon, S. and Straub, B. Pro Git. Apress.
Loeliger, J. and McCullough, M. Version control with Git. O’Reilly.
```

![](img/14.png)

<a name = "item8"></a>
# **Ejercicio 8**
---
![](img/15.png)

Fusionamos la rama bibliografía y la rama main. Para ello añadimos todos los cambios a la zona temporal y realizamos un commit.

![](img/16.png)

Nos dice que hay un problema, asique tendremos que ver las diferencias de las dos ramas y arreglarlas.

![](img/17.png)
![](img/18.png)

Para arreglarlo, tenemos que eliminar las líneas sobrantes del fichero bibliografía.



Añadimos los cambios a la zona temporal, realizamos el commit y mostramos la historia del repositorio de todas las ramas.

![](img/19.png)
