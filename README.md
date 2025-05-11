# API de Machine Learning con Docker

Este repositorio contiene los archivos necesarios para ejecutar una API REST desarrollada con Flask, que utiliza modelos de Machine Learning. El entorno está configurado para correr en Docker utilizando Docker Desktop y Docker Compose.

## Requisitos

Antes de comenzar, asegúrate de tener instalado:

- Docker Desktop


## Estructura del proyecto

Se debe crear una carpeta para el proyecto que contenga la siguiente estructura con los archivos mencionados

<pre> 
 /machine__learning_api/
│
├── models
    ├── model_logistic.h5
    ├── model_forest.h5
    ├── model_svm.h5
    ├── model_tree.h5
├── app.py
├── iris_models.py
└── requirements.txt 
</pre>

## Agregar archivos de configuración Docker

Se deben crear las configuraciones para los archivos `Docker` y `docker-compose.yml` en la carpeta raíz del proyecto, en este caso `machine__learning_api`.

Archivo `Docker`
Este archivo define la imagen personalizada que contiene el entorno necesario para ejecutar la API.

<pre> 
FROM python:3.10

WORKDIR /app

# Copiar archivos
COPY app.py .
COPY models/ ./models/

# Instalar dependencias
RUN pip install flask joblib scikit-learn

EXPOSE 5001

# Comando de inicio  
CMD ["python", "app.py"]  
</pre>

-`FROM python:3.10`: Usa la imagen oficial de Python 3.10 como base.  
-`WORKDIR /app`: Establece el directorio de trabajo dentro del contenedor.  
-`COPY app.py .`: Copia el archivo principal de la API al contenedor.  
-`COPY models/ ./models/`: Copia la carpeta que contiene los modelos al contenedor.  
-`RUN pip install flask joblib scikit.learn`: Instala las dependencias encesarias.  
-`EXPOSE 5001`: Exopne el puerto 5001 en el contenedor (puerto donde se ejecutará Flask).  
-`CMD ["python", "app.py"]`: Ejecuta la aplicación Flas al iniciar el contenedor.  


Archivo `docker-compose.yml`  
docker-compose permite definir y levantar la aplicación con unn solo comando.  

<pre> 
version: "3.8"

services:
 iris-api:
   build:
   ports:
    - "5001:5001"
   volumes:
    - ./models:/app/models
</pre>


-`version: "3.8"`: Define la versión del archivo de configuración.  
-`service`: Lista los servicios a levantar (cada uno se convierte en un contenedor).  
-`iris-api`: Nombre del servicio de la API.  
-`build: .`: Indica que se construya la imagen usando el Dockerfile del directorio actual.  
-`ports`: Mapea el puerto 5001 del contenedor al puerto 5001 del host.  
-`volumes`: Monta la carpeta 'models' de la máquina local dentor del contenedor.  
 





