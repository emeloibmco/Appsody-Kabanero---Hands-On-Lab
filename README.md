
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
*Si ya se encuentra en la lista del repositorio kabanero como libreria principal, seguir a la sección 3 de creación de proyecto*

4. Usamos la CLI de Appsody para agregar la collección a la lista de repositorios con el siguiente comando:

```
	appsody repo add kabanero https://github.com/kabanero-io/collections/releases/download/0.2.1/kabanero-index.yaml
```
5. Verificamos nuevamente que se halla agregado correctamente la colección de Kabanero dentro de la lista de repositorios con el comando:
```
	appsody repo list
```
6. Cuando ya se encuentra durante la 

<a name="proy"></a>  
## 3. Creación proyecto  

sometext

<a name="front"></a>  
## 4. Construcción FrontEnd con NodeJS  

sometext

<a name="back"></a>  
## 5. Construcción BackEnd con SpringBoot2

sometext

<a name="depBack"></a>  
## 6. Despliegue BackEnd con OpenShift y Appsody 

sometext

<a name="depFront"></a>  
## 7. Despliegue FrontEnd con OpenShift y Appsody 

sometext
