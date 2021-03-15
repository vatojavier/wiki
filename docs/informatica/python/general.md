# Bucles óptimos

## List comprehension

### if/else
```python

lista = [f(x) if condition else g(x) for cosa in cosas]

```

### Solo if
```python

lista = [f(x) for cosa in cosas if condition]

```

## Breakpoint con saltos de linea

`pip install ipython`

En el breakpoint poner:

```
(pdb) from IPython import embed; embed()
```

## Timezones y esas cosas

Convertir a timezone, le dices que timezone es y lo conviertes:

```python
date = date(2021, 3, 9)

# ahora le pones la hora (00:00 de ese día)
date_time = datetime.combine(date, datetime.min.time())  # last_date a 00:00:00, tambien se puede hacer directo el datetime

# le especificas y lo conviertes
target_time_zone = pytz.timezone("Europe/Madrid")
date_time.replace(tzinfo=pytz.utc).astimezone(target_time_zone).strftime('%d-%m-%Y %H') # con el dia y la hora
```
