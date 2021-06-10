
## `COUNT` con condición sin utilizar un `WHERE`

```sql
SELECT sum(if(t.cost_premium_insurance > 0, 1, 0)) as viajesConSeguro
FROM TABLA_WAPA
```
