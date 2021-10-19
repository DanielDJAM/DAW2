Daniel de Jesús Álvarez Miranda		2º DAW

# Servicios RESTful con Tomcat y Jersey (incompleto)

## Apreciaciones de la práctica incompleta de despliegue de un servicio rest con apache-tomcat.


Al lanzar el comando “mvn clean install”, crea el proyecto con sus librerías. La cuestión es que como vemos en la imagen, hay un problema de acceso a una librería llamada guise.jar.

Al buscar por internet, no encontré nada muy claro. Simplemente que se alojaba en .m2 que es como la carpeta de configuración de maven. También una solución era modificar el pom.xml pero como dijo nuestro profesor en clase, este fichero no se toca, solo se mira.

![](img/01.png)

Aunque saltase este error, el proyecto se creaba como podemos observar.

![](img/02.png)


Al intentar desplegar, usábamos el comando “mvn tomcat10:deploy” (usaba tomcat10 porque era la versión que tenía pero más adelante me di cuenta que era un error), y había un error al construirse. Dicho error era que faltaba los plugins “org.apache.maven.plugins” y “org.codehaus.mojo”. Siendo sinceros, sabía que debía de poner las librerías faltantes en *“/opt/tomcat/lib” o “web-apps/lib”.* Mi cuestión es, qué es una librería y como ponerla en dicha carpeta. Si una librería es lo que se pone en el pom.xml, entonces ¿Tendría que hacer lo mismo?.

![](img/03.png)

Si lanzamos el comando “mvn tomcat7:deploy” nos sale un error distinto y no sé explicar mucho más de lo que sale en la imagen.

![](img/04.png)

Al no saber que es lo que sale en la imagen, voy a mirar los logs en “/opt/tomcat/apache-tomcat/logs”. Buscamos en “catalina.2021-10-19.log”.


![](img/05.png)


Nos sale que falta una librería de apache donde podríamos suponer, de disponer de ella, iría en “/opt/tomcat/apache-tomcat/libs” .

![](img/06.png)

Si entramos en “localhost.2021-10-19.log” no encontramos nada interesante.

![](img/07.png)


Si miramos “localhost\_access\_log.2021-10-19.txt” vemos que lo único destacable es lo siguiente pero tampoco sé qué hacer con ello.

![](img/08.png)

CONCLUSIÓN: No he llegado a entender nada de esta práctica aún que haya estado investigando en mil páginas, ya sea en inglés o otros idiomas. Creo fervientemente que estoy mucho más liado que al principio y después de pasarlo tan mal porque no conseguí resolver ningún error, no me gustaría volver a pasar por esto y si tuviera que hacerlo, no sería nada satisfactorio.
