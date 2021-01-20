# Postgres

Después de instalarlo como dice la página puede dar el error:

`
psql: error: FATAL:  Peer authentication failed for user "postgres"
`

Entonces cambiar la linea del archivo `/etc/postgresql/13/main/pg_hba.conf`

de

`local   all             postgres                                peer`

a

`local   all             postgres                                md5`




## psql

### Lista las DB

```
psql -U postgres -l
```

### Comandos dentro de psql

Listar DBs: ```\l```
Listar usuarios: ```\du```
