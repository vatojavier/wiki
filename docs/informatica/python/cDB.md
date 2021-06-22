# Conexiones a bases de datos usando python

## SQLAlchemy
### MySQL

`pip install sqlachemy`

`pip install mysqlclient`

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


