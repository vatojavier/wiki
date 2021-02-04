# Conexiones a bases de datos usando python

## MySQL

### SQLAlchemy

`pip install sqlachemy`

`pip install mysqlclient`

```python
from sqlalchemy import create_engine

engine = create_engine("mysql+mysqldb://user:password@ip:3306/DB")

```
