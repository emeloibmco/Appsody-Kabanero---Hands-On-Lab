
# Guía Appsody-Kabanero
En esta guía se hará un Hands On de la construcción y despliegue de un aplicativo web desarrollado de manera nativa para la nube con el uso de las tecnologías como Appsody, Kabanero y OpenShift.


## Tabla de contenidos :clipboard:

1. [ Instalación Appsody. ](#instApp)  
2. [Configuración Appsody con Kabanero. ](#instKab)  
3. [ Creación proyecto. ](#proy)  
4. [ Construcción FrontEnd (Node JS). ](#front)  
5. [ Construcción BackEnd (SpringBoot2). ](#back)  
6. [ Despliegue BackEnd con OpenShift. ](#depBack)
7. [ Despliegue FrontEnd con OpenShift. ](#depFront)  

## Pre-requisitos

 - Tener Docker instalado localmente en la máquina o instalar desde el  [ Docker Installation](https://docs.docker.com/get-docker/).
 - Tener la CLI de IBM Cloud en el computador o instalar desde [Instalación CLI IBM Cloud](https://cloud.ibm.com/docs/cli).
 - Tener la CLI de OpenShift OC en la máquina o instalar desde [Descarga Openshift CLI ](https://www.okd.io/download.html)
   
<a name="instApp"></a>  
## 1. Instalación Appsody   
  
1. Ingresar a la URL :
      [https://appsody.dev/docs/installing/installing-appsody](https://appsody.dev/docs/installing/installing-appsody) 
 
 2. Seleccionar el sistema operativo para abrir la guía de instalación de Appsody.

3. Seguir el paso a paso de la instalación de Appsody.

 4. Verificar la correcta instalación de Appsody en la terminal o CMD del dispositivo:
 
```
    appsody version
```
Resultado similar al siguiente:

```
    appsody 0.6.4
```
<a name="instKab"></a>  
## 2. Configuración Appsody con Kabanero  
  
1. Acceder al cluster de OpenShift con Cloud Pak for Applications. 
2. Acceder a la sección brindada por el Cloud Pak for Applications y copiar la url desde el Collection Hub de  Kabanero Collections, tal como la siguiente:
```
	https://github.com/kabanero-io/collections/releases/download/v0.1.2/kabanero-index.yaml
```
3. Acceder a la lista de repositorios de Appsody para verificar si Kabanero se encuentra como libreria de repositorios principal de appsody con el siguiente comando:
```
	appsody repo list
```
Respuesta:
```
	% appsody repo list

	NAME  URL
	*incubator  https://github.com/appsody/stacks/releases/latest/download/incubator-index.yaml
	experimental  https://github.com/appsody/stacks/releases/latest/download/experimental-index.yaml
```

4. Usamos la CLI de Appsody para agregar la collección a la lista de repositorios con el siguiente comando:

```
	appsody repo add kabanero https://github.com/kabanero-io/collections/releases/download/0.2.1/kabanero-index.yaml
```
5. Verificamos nuevamente que se halla agregado correctamente la colección de Kabanero dentro de la lista de repositorios con el comando:
```
	appsody repo list
```
Respuesta:
```
	% appsody repo list

	NAME  URL
	*incubator  https://github.com/appsody/stacks/releases/latest/download/incubator-index.yaml
	experimental  https://github.com/appsody/stacks/releases/latest/download/experimental-index.yaml
	kabanero  https://github.com/kabanero-io/collections/releases/download/0.2.1/kabanero-index.yaml
```
6. Cuando ya se encuentra dentro de la lista de repositorios es necesario colocar Kabanero Collections como el repositorio por defecto de Appsody para que sea más fácil el acceso al mismo, por lo tanto se escribe el siguiente comando:
```
	appsody repo set-default kabanero
```
7. Se comprueba nuevamente que Kabanero sea el repositorio por defecto de Appsody donde al lado del nombre y del link aparezca un * que lo identifique como el principal, con el siguiente comando:
```
	appsody repo list
```
Respuesta:
```
	%  appsody repo list
	
	NAME  URL
	*kabanero https://github.com/kabanero-io/collections/releases/download/0.2.1/kabanero-index.yaml
	experimental  https://github.com/appsody/stacks/releases/latest/download/experimental-index.yaml
	incubator https://github.com/appsody/stacks/releases/latest/download/incubator-index.yaml
```
8. Ahora se puede comprobar los distintos tipos de repositorios apilados que contiene Kabanero Collections como parte de su desarrollo nativo para la nube, estos se pueden observar con el siguiente comando:

```
	appsody list kabanero
```

```
	% appsody list kabanero

	REPO       ID VERSION  	  TEMPLATES     DESCRIPTION
	kabanero  java-microprofile  0.2.18 *default Eclipse MicroProfile on Open Liberty & OpenJ9 using Maven
	kabanero  java-spring-boot2  0.3.15 *default, kotlin Spring Boot using OpenJ9 and Maven
	kabanero  nodejs 0.2.5  *simple  Runtime for Node.js applications
	kabanero  nodejs-express 0.2.7  scaffold, *simple  Express web framework for Node.js
	kabanero  nodejs-loopback  0.1.5  *scaffold  LoopBack 4 API Framework for Node.js
```
<a name="proy"></a>  
## 3. Creación proyecto  

En esta sección del HandsOn se va a construir el producto final donde se creara el proyecto y se clonara en de manera local los archivos de este github.

1. Hay que ir a la carpeta inicial del computador donde se va a crear el desarrollo, en este ejemplo se va a realizar en la carpeta base del computador.
2. Hay que crear dos carpetas que lleve por nombre una Quote-Application y la otra Git-App, esto para crear el despliegue que se la carpeta Quote-Application y la otra para clonar los archivos de este github en la maquina. 
3. Dentro de la carpeta Quote-Application se crean dos carpetas más una para el FrontEnd y la otra para el BackEnd.
4. Ahora hay que clonar las carpetas de este github desde la terminal o CMD del computador, con el siguiente comando:
```
	cd Git-App 
	git clone https://github.com/emeloibmco/Appsody-Kabanero-Hands-On-Lab.git
```    

<a name="front"></a>  
## 4. Construcción FrontEnd con NodeJS  

1. Acceder a la carpeta del proyecto desde la CMD o terminal y desde ahí acceder a la carpeta del FrontEnd.
```
	cd Quote-Application/FrontEnd	
```
2. En este paso se va a crear un proyecto utilizando la CLI de Appsody para aligerar el desarrollo nativo de nube, como se observó en pasos anteriores, dentro de los repositorios de Kabanero se encuentra el repositorio de NodeJs que es el lenguaje en donde esta desarrollado el FrontEnd de la aplicación, por lo tanto se inicia con el siguiente comando:

```
		appsody init kabanero/nodejs-express
```
3. Al terminar el comando de appsody init se puede listar el contenido de la carpeta y se puede observar que hay nuevo archivos dentro de la misma que son archivos establecidos por Kabanero para una aplicación minimo de NodeJS con Express.

```
	% ls

	app.js  package-lock.json  package.json  test
```
4. Con Appsody es posible correr localmente y de inmediato el proyecto sin utilizar librerías externas del lenguaje de desarrollo utilizado, solo utilizando el comando:
```
	appsody run
```
Resultado:
	`App started on PORT 3000`

Con esto se puede acceder a la direccion http://localhost:3000 desde cualquier navegador y se ve el proyecto base para el front creado con Appsody.

 El stack de appsody con NodeJs y Express desde Kabanero, tiene un plus que permite mostrar desde adentro como puede ser el comportamiento de la aplicación con métricas desde los endpoint y el performance del aplicativo, para estoy hay varias url de acceso de manera local que muestran el comportamiento tales como:
 - Endpoint de Salud: http://localhost:3000/health
 - Endpoint de Vida: http://localhost:3000/live
 - Endpoint de Terminación: http://localhost:3000/ready
 - Endpoint de Métricas: http://localhost:3000/metrics
 - Endpoint del Dashboard: http://localhost:3000/appmetrics-dash 

 
<a name="back"></a>  
## 5. Construcción BackEnd con SpringBoot2



<a name="depBack"></a>  
## 6. Despliegue BackEnd con OpenShift y Appsody 



<a name="depFront"></a>  
## 7. Despliegue FrontEnd con OpenShift y Appsody 
