Daniel de Jesús Álvarez Miranda		2º DAW


# CLUSTERIZANDO UNA APP EN WILDFLY



## Indice

[Desplegando un Cluster de JBOSS con Docker](#item1)

[Construcción del proyecto](#item2)


<a name = "item1"></a>

## Desplegando un Cluster de JBOSS con Docker

Haremos uso de la imagen de docker de WildFly que vimos anteriormente. También haremos uso de Docker compose, construyendo un cluster a medida para las necesidades de nuestra aplicación.

<a name = "item2"></a>

### Construcción del proyecto

Modificamos web.xml. Cambiamos la línea “   <display-name>app-web-alumno</display-name>  ” por nuestro nombre.

![](img/01.png)


Lanzamos el siguiente  comando para construir el proyecto.

![](img/02.png)

Una vez construido, podemos ver el resultado ejecutando el modo local.

```console
mvn clean jetty:run
```

![](img/03.png)

Vamos a un navegador y comprobamos.

![](img/04.png)


Construiremos el fichero Dockerfile dentro de la carpeta de nuestra aplicación. Este fichero tendrá lo siguiente:

```console

FROM jboss/wildfly

ARG WAR_FILE=target/*.war

##COPY ${JAR_FILE} app.jar

ADD ${ARG} /opt/jboss/wildfly/standalone/deployments/

ARG WILDFLY_NAME

ARG CLUSTER_PW

ENV WILDFLY_NAME=${WILDFLY_NAME}

ENV CLUSTER_PW=${CLUSTER_PW}

ENTRYPOINT /opt/jboss/wildfly/bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0 -Djboss.server.default.config=standalone-full-ha.xml -Djboss.node.name=${WILDFLY_NAME} -Djava.net.preferIPv4Stack=true -Djgroups.bind_addr=$(hostname -i) -Djboss.messaging.cluster.password=${CLUSTER_PW}

```

![](img/05.png)



También debemos crear el fichero .yml para la construcción del cluster.

```console

version: '3.5'

services:

wildfly1:

build:

context: .

args:

WILDFLY_NAME: wildfly_1

CLUSTER_PW: secret_password

image: wildfly_1

ports:

- 8080:8080

networks:

wildfly_network:

wildfly2:

build:

context: .

args:

WILDFLY_NAME: wildfly_2

CLUSTER_PW: secret_password

image: wildfly_2

ports:

- 8081:8080

networks:

wildfly_network:

networks:

wildfly_network:

ipam:

driver: default

```

![](img/06.png)



Para finalizar, creamos el cluster de dos nodos con el siguiente comando y comprobamos.

```console
docker-compose up
```

![](img/07.png)
