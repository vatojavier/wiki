# Docker
Ejemplo desplegar y ejecutar una aplicación con Docker:

### Dockerfile
Tener un Dockerfile y un `requirements.txt`.

`ENTRYPOINT` será el comando a ejecutar cuando se eejecute el Docker.

```Dockerfile
FROM python:3.8-slim-buster
RUN apt-get update && apt-get upgrade -y && rm -rf /var/lib/apt/lists/*
RUN pip install pip --upgrade
RUN mkdir /app
RUN mkdir /app/logs

COPY . /app/

WORKDIR /app
RUN pip install -r requirements.txt

WORKDIR /app
ENTRYPOINT ["python", "send_mail.py"]
```
