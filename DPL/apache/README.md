﻿Daniel de Jesús Álvarez Miranda		2º DAW



# Instalación de Apache en Linux



## Indice
---
[Previo](#item1)
[Instalación Apache](#item2)
[Acceso](#item3)


<a name = "item1"></a>
## Previo
---

Antes de empezar, debemos asegurarnos que tenemos todo el sistema actualizado.

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.001.png)


<a name = "item2"></a>
## Instalación Apache
---

Descargamos e instalamos Apache2.

```console

sudo apt install apache2

```

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.002.png)

Si nos encontramos con el siguiente problema, podemos solucionarlo a continuación.

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.003.png)

El problema es debido a que el puerto 80 ya está siendo utilizado por otro programa. Por lo que tendremos que decirle que use otro diferente. Para ello tendremos que ir a un archivo de contiguración. Podemos hacerlo con el siguiente comando.

```console

sudo nano /etc/apache2/ports.conf

```

Dentro del fichero cambiamos el Listen 80 por 8081.

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.004.png)

Tendremos que hacer lo mismo en el siguiente fichero. Cambiamos 80 por 81.

```console

sudo nano /etc/apache2/sites-enabled/000-default.conf
```

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.005.png)


Reiniciamos los servicios de Apache y comprobamos que está activo.

```console

sudo systemctl restart apache2

sudo systemctl status apache2

```

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.006.png)

Ajustamos la configuración del firewall. Usamos el siguiente comando.

```console

sudo ufw app list

```

Después veremos el siguiente mensaje.

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.007.png)


| Aplicación | Descripción |

| ------------- | ------------- |

| Apache  | Apertura solo del puerto 80, que permite trafico sin cifrar (No seguro).  |

| Apache Full  | Apertura tanto del puerto 80 como del puerto 443, permitiendo el tráfico cifrado (Seguro) |

| Apache Secure  | Apertura solo del puerto 443, permitiendo conexiones seguras (HTTPS) |


Añadimos una regla al firewall para que no restrinja el uso de Apache.

```console

sudo ufw allow 'Apache'

```

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.008.png)


Tendremos que ver el estado del firewall. Para ello recurrimos al siguiente comando. De estar inactivo, tendremos que habilitarlo.

```console

sudo ufw status

sudo ufw enable

```

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.009.png)

Volvemos a comprobar.

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.010.png)


Ahora comprobamos que el estado de Apache2 esté funcionando correctamente.

```console

sudo systemctl status apache2

```

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.011.png)

<a name = "item3"></a>
## Acceso
---

Para comprobar que todo está correctamente, vamos al navegador y entramos por el puerto que acabamos de configurar. En nuestro caso, el puerto 8081.

![](Aspose.Words.ffb2695a-0132-4d99-adc2-ff881c74bca1.012.png)