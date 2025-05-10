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

<pre>``` 
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
```</pre>

