Daniel de Jesús Álvarez Miranda DAW – 2º B

` `**Instalar G  IT** 

**Sumario**

1. [Descargar e instalar Git....................................................................................................................3](#_page1_x56.70_y110.45)
1. [Configurando el Git..........................................................................................................................4](#_page2_x56.70_y110.45)
1. **Descargar e instalar Git.**

Primero debemos comprobar si nuestro Sistema Operativo (SO) ya tiene esta aplicación. Para ello, usaremos el comando:

git - -version

Si lo tenemos instalado, nos saldrá una versión de dicha aplicación. De lo contrario, empezaremos la descarga e instalación de la misma con el siguiente comando:

sudo apt install git

![](img/01.png)

Una vez instalado, comprobamos que todo está correctamente al comprobar su versión. git --version

![](img/02.png)

2. **Configurando el Git.**

Para que nuestros mensajes de confirmación tengan más información de quién los ha realizado, configuraremos nuestro git con nuestro nombre y nuestro email. Así, cada vez que hagamos un cambio, podrán saber quien ha sido y tengan algún método de comunicación poniendo nuestro email.

git config --global user.name "Your Name"![](img/03.png)

git config --global user.email "youremail@domain.com"

Si queremos cambiar algún valor de los anteriores o añadir uno nuevo, solo tendremos que ir al archivo de gitconfig y con un editor de texto, modificar su contenido.

nano ~/.gitconfig

![](img/04.png)
