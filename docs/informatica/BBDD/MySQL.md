
## `COUNT` con condición sin utilizar un `WHERE`

```sql
SELECT sum(if(t.cost_premium_insurance > 0, 1, 0)) as viajesConSeguro
FROM TABLA_WAPA
```

## Condición de columna en where
Dependiendo de algún campo, la condición del where puede depender de una columna u otra:

**Solo meter un `case` en el where con la condición y seleccionando la columna**

```sql
select *
from TABLAS_Y_JOINS
WHERE
(case
  when refund_id is null and gc.payment_id is not null then
    pa.created_at
  when refund_id is null and gc.payment_id is null then
    gc.created_at
  WHEN refund_id is not null then
    pa2.created_at
end
) >= '{start_date}'
```

## Show processes and kill them

```MYSQL
SHOW PROCESSLIST;

KILL 38239;
KILL 38240;

-- To make it more automatically
SELECT concat('KILL ',id,';') FROM information_schema.processlist;

-- And execute the output one by one

```


