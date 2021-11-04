# Conexiones a bases de datos usando python

## SQLAlchemy
### MySQL

`pip install sqlachemy`

`pip install mysqlclient`

Puede que necesites antes:
```
sudo apt-get install libmysqlclient-dev
sudo apt-get install python3-dev default-libmysqlclient-dev build-essential
```

```python
from sqlalchemy import create_engine

engine = create_engine("mysql+mysqldb://user:password@ip:3306/DB")

```

### Postgres
Los dialectos de postgres:

`pip install psycopg2-binary`

`pip install psycopg2`

Si sigue dando problemas  (seguramente por python 3.9 no soportado)

`
sudo apt install python3-dev libpq-dev
`

String de conexión:

`export SQLALCHEMY_DATABASE_URI=postgresql://user:pass@ip:5432/databasename`

### Execute statement
```python
command = """
UPDATE motit.`User` u
set u.city_id = 1
where u.id in {users}
"""

users = tuple(df_usuarios_zara['id'].to_list())

with mysql_engine.connect() as con:
    con.execute(command.format(users=users))
```
