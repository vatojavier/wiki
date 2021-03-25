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

### Tambien: 

```python
date_interest = date(2021, 3, 28)

# Date previous (7 days)
date_interest_previous = date_interest - timedelta(days=7)

local_tz = pytz.timezone("Europe/Madrid")

# From y to de la actual
date_interest_time_init = datetime.combine(date_interest, datetime.min.time())  # last_date a 00:00:00
date_interest_time_to = (
    local_tz.localize(date_interest_time_init.replace(hour=hour)).astimezone(pytz.utc).replace(tzinfo=None)
)

# From y to de la previous
date_interest_time_init_previous = datetime.combine(date_interest_previous, datetime.min.time())  # prev a 00:00:00
date_interest_time_to_previous = (
    local_tz.localize(date_interest_time_init_previous.replace(hour=hour)).astimezone(pytz.utc).replace(tzinfo=None)
)

```

