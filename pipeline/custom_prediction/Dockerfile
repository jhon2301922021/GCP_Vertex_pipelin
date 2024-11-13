# Usa la imagen base de Python 3.9
FROM python:3.9

# Evita que Python genere archivos .pyc
ENV PYTHONDONTWRITEBYTECODE=1

# Expone el puerto 8080
EXPOSE 8080

# Establece el entrypoint para iniciar el servidor de predicción de AI Platform
ENTRYPOINT ["python", "-m", "google.cloud.aiplatform.prediction.model_server"]

# Crea los directorios necesarios con permisos para todos los usuarios
RUN mkdir -m 777 -p /usr/app /home
WORKDIR /usr/app
ENV HOME=/home

# Instala el paquete google-cloud-aiplatform con el extra de prediction
RUN pip install --no-cache-dir --force-reinstall 'google-cloud-aiplatform[prediction]>=1.16.0'

# Define las variables de entorno para los módulos y clases del predictor
ENV HANDLER_MODULE=google.cloud.aiplatform.prediction.handler
ENV HANDLER_CLASS=PredictionHandler
ENV PREDICTOR_MODULE=predictor
ENV PREDICTOR_CLASS=CprPredictor

# Copia el directorio de origen al contenedor
COPY [".", "."]

# Instala las dependencias del archivo requirements.txt
RUN pip install --no-cache-dir --force-reinstall -r requirements.txt
