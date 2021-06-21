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
## Desplegar
`deployMail.sh`
```bash
cd /home/elvato

# O si quieres desde un repo de git
#cd /GIT/aad_datascience__reporte-diario
#git fetch --all
#git reset --hard origin/develop
#git pull origin develop

docker build -t reporte-mail:1.0 .
```

## Ejecutar
`executeMail.sh`

```bash
#!/bin/bash

docker rm -f reporte-mail

docker run \
  --name reporte-mail \
  -e VAR1="VAR1" \
  -e "VAR2=VAR2" \
  -e "LOGS_PATH=/app/logs" \
  -v /var/log/reporte-mail/:/app/logs \
  reporte-mail:1.0 > /home/elvato/log.txt
```


