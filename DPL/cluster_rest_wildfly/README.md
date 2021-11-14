Daniel de Jesús Álvarez Miranda		2º DAW


# MODIFICANDO Y CLUSTERIZANDO UN SERVICIO REST EN WILDFLY



## Indice

[Esquema del proyecto.](#item1)

[Docker-compose.](#item2)

[LAMP.](#item3)

[Base de Datos.](#item4)

[WildFly.](#item5)

[Despliegue.](#item6)

[Comprobamos.](#item7)


<a name = "item1"></a>

## Esquema del proyecto.

Nuestro proyecto va a tener una estructura como la siguiente.

![](img/01.png)

![](img/02.png)


<a name = "item2"></a>

## Docker-compose.

Nuestro docker-compose va a tener la siguiente configuración:

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
     - default

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
     - default
  
  wildfly3:
    build:
      context: .
      args:
        WILDFLY_NAME: wildfly_3
        CLUSTER_PW: secret_password
    image: wildfly_3
    ports:
    - 8082:8080
    networks:
     - default
     
  www:
    build: lamp/.
    ports:
     - "80:80"
    volumes:
     - ./www:/var/www/html
    links:
     - db
    networks:
     - default
  db:
    image: mysql:8.0
    ports:
      - "3306:3306"
    command: --default-authentication-plugin=mysql_native_password
    environment:
      MYSQL_DATABASE: dbname
      MYSQL_PASSWORD: test
      MYSQL_ROOT_PASSWORD: test
    volumes:
      - ./dump:/docker-entrypoint-initdb.d
      - ./conf:/etc/mysql/conf.d
      - persistent:/var/lib/mysql
    networks:
      - default
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    links:
      - db:db
    ports:
      - 8000:80
    environment:
      MYSQL_PASSWORD: test
      MYSQL_ROOT_PASSWORD: test

volumes:
  persistent:
```

**build:** Es donde se encuentra el archivo Dockerfile.

**Volumes:** Es donde tenemos guardada nuestra configuración.

**Ports:** Puertos que utilizará docker.


<a name = "item3"></a>

## LAMP.

Una vez creado el docker-compose, crearemos un directorio que se llamará lamp. Dentro de él, crearemos un Dockerfile para la instalación de un Apache, Mysql y PHP.

```console
FROM php:8.0.0-apache
ARG DEBIAN_FRONTEND=noninteractive
RUN docker-php-ext-install mysqli
RUN apt-get update \
    && apt-get install -y libzip-dev \
    && apt-get install -y zlib1g-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install zip

RUN a2enmod rewrite
```

![](img/03.png)


<a name = "item4"></a>

## Base de Datos.

Crearemos un directorio que se llamará “dump”. Dentro tendremos un fichero sql con la siguiente configuración.

```console
  SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
  SET time_zone = "+00:00";

  /*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
  /*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
  /*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
  /*!40101 SET NAMES utf8mb4 */;

  CREATE TABLE `Data` (
    `id` int(11) NOT NULL,
    `name` varchar(20) NOT NULL
  ) ENGINE=InnoDB DEFAULT CHARSET=latin1;

  INSERT INTO `Data` (`id`, `name`) VALUES (1, 'OpenWebinars Article'), (2, 'Crashell'), (3, 'Jerson Martinez'
), (4, 'Antonio Moreno');

  /*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
  /*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
  /*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
```


![](img/04.png)


<a name = "item5"></a>

## WildFly.

Para nuestro servidor de despliegue, usaremos WildFly. Para ello, creamos un Dockerfile en la raíz de nuestro proyecto o en un directorio al mismo nivel o superior que nuestro **.war**. Dentro de dicho fichero, pondremos la instalación y configuración de WildFly.

```console

FROM jboss/wildfly

ARG WAR_FILE=target/*.war
##COPY ${JAR_FILE} app.jar

ADD ${WAR_FILE} /opt/jboss/wildfly/standalone/deployments/

ARG WILDFLY_NAME
ARG CLUSTER_PW

ENV WILDFLY_NAME=${WILDFLY_NAME}
ENV CLUSTER_PW=${CLUSTER_PW}

ENTRYPOINT /opt/jboss/wildfly/bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0 -Djboss.server.default.config=
standalone-full-ha.xml -Djboss.node.name=${WILDFLY_NAME} -Djava.net.preferIPv4Stack=true -Djgroups.bind_addr=$
(hostname -i) -Djboss.messaging.cluster.password=${CLUSTER_PW}

```


![](img/05.png)


<a name = "item6"></a>

## Despliegue.

Una vez tengamos todos los archivos creados, iremos a la ubicación de nuestro proyecto mediante una consola e introducimos lo siguiente:

```console
mvn clean install
```

Una vez finalizada, vamos a la ubicación de nuestro docker-compose y lanzamos el comando para que se instalen y configuren los dockers que hemos preparado.

```console
sudo docker-compose up -d
```

![](img/06.png)

Si nos ha dado algún error, debemos de eliminar todas las imágenes y contenedores que se hayan creado para que no nos salte otro error. Para ello podemos usar lo siguiente:

```console
sudo docker-compose down -v --remove-orphans  --rmi all
```


<a name = "item7"></a>

## Comprobamos.

Una vez que nuestros contenedores estén funcionando, debemos comprobar que está todo correctamente. Para ello tenemos que probar nuestro phpMyAdmin (localhost:8000), WildFly (localhost:8081) y nuestra página html (localhost:8081/helloworld-rs).

![](img/07.png)

![](img/08.png)

![](img/09.png)

![](img/10.png)
