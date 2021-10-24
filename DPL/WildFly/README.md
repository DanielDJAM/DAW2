Daniel de Jesús Álvarez Miranda		2º DAW


# INSTALACIÓN JBOSS-WILDFLY


## INDICE

[Instalación de WildFly	2](#item1)

[Configurar a WildFly	8](#item2)

[Acceso a WildFly	10](#item3)

[Añadir usuarios.	11](#item4)

[Gestionar la consola.	14](#item5)


<a name = "item1"></a>
## Instalación de WildFly

### Descarga

Descargamos el paquete correspondiente. Nosotros usaremos el comando wget y la versión 25 de WildFly.

```console

wget https://github.com/wildfly/wildfly/releases/download/25.0.0.Final/wildfly-25.0.0.Final.tar.gz

```

![](img/01.png)

### Grupo y Usuario

Creamos el grupo y usuario wildfly.

```console

sudo groupadd -r wildfly

sudo useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly

```

![](img/02.png)

### Descomprimir y Enlazar

Descomprimimos el paquete que descargamos con wget.

```console

tar -xvzf wildfly-25.0.0.Final.tar.gz

```

![](img/03.png)

Movemos el archivo descomprimido a la ruta deseada y creamos un enlace simbólico.

```console

sudo mv wildfly-25.0.0.Final /opt/wildfly-25.0.0.Final

```

![](img/04.png)sudo ln -s /opt/wildfly-25.0.0.Final /opt/wildfly


### Acceso

Damos acceso al usuario y grupo wildfly.

```console

sudo chown -R wildfly:wildfly /opt/wildfly

sudo chown -R wildfly:wildfly /opt/wildfly/

```

![](img/05.png)

Configurar e Iniciar

```console

sudo mkdir -p /etc/wildfly

sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly/

```

![](img/06.png)

### Fichero de arranque

En la siguiente ruta, podemos encontrar la configuración de arranque donde estará por defecto en standalone.

```console

sudo nano /etc/wildfly/wildfly.conf

```

![](img/07.png)

Configurar Arranque

Para configurar el arranque, lanzamos los siguientes comandos:

```console

sudo cp /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin/

sudo sh -c 'chmod +x /opt/wildfly/bin/\*.sh'

sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system/

sudo systemctl daemon-reload

```

![](img/08.png)


### Iniciar y Verificar

Una ver guardado el archivo, iniciamos el archivo con el siguiente comando. Luego verificamos que está todo correctamente.

```console

sudo systemctl start wildfly

sudo systemctl status wildfly

```

![](img/09.png)

### Inicio Automático

Si queremos que inicie automáticamente, tendremos que habilitarlo del siguiente modo:

```console

sudo systemctl enable wildfly

```

![](img/10.png)

<a name = "item2"></a>

## Configurar a WildFly

Permitiremos el tráfico por el puerto que queramos. En nuestro caso lo pondremos en el 8083. Para modificarlo, tendremos que ir al siguiente fichero:

```console

sudo nano /opt/wildfly/standalone/configuration/standalone.xml

```

![](img/11.png)

Y modificar la etiqueta:

```console

<socket-binding name="http" port="${jboss.http.port:8080}"/>

```

por

```console

<socket-binding name="http" port="${jboss.http.port:8083}"/>

```

![](img/12.png)


Y habilitamos la regla en el cortafuegos de que permita conexiones a través de ese puerto.

```console

sudo ufw allow 8083/tcp

```

![](img/13.png)

<a name = "item3"></a>

## Acceso a WildFly

Para acceder a wildfly, tenemos que ir a un navegador y poner la dirección del servidor y su puerto. En nuestro caso será localhost y el puerto 8083.

![](img/14.png)

<a name = "item4"></a>

## Añadir usuarios.

Creamos el usuario administrador.

```console

sudo /opt/wildfly/bin/add-user.sh

```

He tenido problemas al crear dicho usuario porque siempre me aparecía dicho error. Estuve indagando en el código add-user.sh y para averiguar que fallaba, modifiqué un poco el código colocando un echo para avisar si pasaba por ese código. El caso es que no me pillaba $JAVA_HOME aunque estaba correcto. Escribía en la consola echo $JAVA\_HOME y me devolvía la ruta sin el *bin al final, pero al lanzar el comando, me decía que sí tenía un bin al final y me daba dicho error. Después de pasarme desde el día (20-10-*21) hasta hoy (24/10/21), pude ver el error. Dicho error era que en “/etc/environment”, el $JAVA_HOME tenía un /bin al final, pero lo curioso es que tenía un script que cambiaba el $JAVA_HOME, y también lo cambié a mano con el export. Todas esas veces me devolvía el valor que quería pero a la hora de lanzar dicho comando, no funcionaba.

![](img/15.png)


Estas son imágenes de lo que hice.

![](img/16.png)

![](img/17.png)


Al final solucioné el error.

![](img/18.png)


Esta es la pantalla completa.

![](img/19.png)

<a name = "item5"></a>

## Gestionar la consola.

Realizamos la siguiente configuración:

```console

sudo nano /etc/wildfly/wildfly.conf

```

![](img/20.png)

Configuramos el siguiente archivo:

```console

sudo nano /opt/wildfly/bin/launch.sh

```



Verificamos que se encuentra lo siguiente:

```console

$WILDFLY\_HOME/bin/domain.sh -c $2 -b $3 -bmanagement $4

else

$WILDFLY\_HOME/bin/standalone.sh -c $2 -b $3 -bmanagement $4

```

![](img/21.png)


Para finalizar, lanzamos los siguientes comandos:

```console

sudo systemctl restart wildfly

sudo nano /etc/systemd/system/wildfly.service

ExecStart=/opt/wildfly/bin/launch.sh $WILDFLY\_MODE $WILDFLY\_CONFIG $WILDFLY\_BIND $WILDFLY\_CONSOLE\_BIND

sudo systemctl daemon-reload

sudo systemctl restart wildfly

```

Aqui vemos el archivo modificado como hemos descrito arriba.

![](img/22.png)


Y aquí todos los comandos lanzados correctamente.

![](img/23.png)

