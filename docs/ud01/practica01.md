
## Instalando AWS CLI 

AWS CLI, es el cliente de AWS mediante el cual podremos utilizar la terminal para poder trabajar con nuestro entorno en lugar de utilizar la herramienta gráfica. 

En este apartado indicaré la página de la documentación desde donde podremos ir siguiendo las instrucciones de instalación: 

[https://docs.aws.amazon.com/es_es/cli/latest/userguide/getting-started-install.html ](https://docs.aws.amazon.com/es_es/cli/latest/userguide/getting-started-install.html)

Desde aquí podremos seleccionar el sistema operativo en el que trabajamos y poder seguir las instrucciones de instalación. 

![](../images/ud01/practica1/015.png)

Una vez finalizada la instalación podremos comprobar la versión instalada mediante el comando `aws --version`. 

![](../images/ud01/practica1/016.png)

## El laboratorio

Teniendo un laboratorio en marcha y el cliente instalado, el siguiente paso es conectarlos. Para ello hay que seguir los siguientes pasos: 

Ver credenciales del laboratorio: 

![](../images/ud01/practica1/017.png)

Haremos click en show: 

![](../images/ud01/practica1/018.png)

Ahora utilizaremos el siguiente comando para enlazar la terminal con el lab. 

``aws configure``  

E iremos copiando y pegando la información que nos vaya pidiendo: 

![](../images/ud01/practica1/020.png)

Una vez configurado comprobaremos si podemos recuperar la información del usuario: 

``aws sts get-caller-identity``

![](../images/ud01/practica1/022.png)

En el caso de los labs vemos que no logra conectarse y devuelve un error. Para paliar este error accederemos a la carpeta personal del usuario y dentro de ésta hay una carpeta oculta .aws (creada cuando hemos hecho aws configure), y dentro de esta carpeta tenemos el archivo credentials, el cual tiene la información que hemos introducido antes. Ahora bien, para arreglarlo vaciaremos el contenido del archivo y copiaremos toda la información de AWS Details dentro del archivo: 

![](../images/ud01/practica1/023.png)

![](../images/ud01/practica1/024.png)

Y una vez hecho comprobaremos si nos devuelve las credenciales: 

![](../images/ud01/practica1/025.png)

Al ser un entorno preparado de laboratorio las credenciales devueltas son de un perfil general (*Estudiante  de  prueba*) pero si fueran credenciales reales devolvería el nombre correspondiente. Destacar que *Arn* significa *Amazon Resource Name* que es el identificador que genera AWS para identificar recursos/servicios. 
