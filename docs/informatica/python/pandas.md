# Pandas

## Aplicar función custom para DF usando Lambda

Añade un nuevo campo al dataframe dependiendo de una condición calculada por función.
Con list comprehension no se pueden utilizar funciones custom.

Se puede acceder al campo de la fila ya sea con `row["campo"]` o `row.campo`
```python
df["mov"] = df.apply(lambda row: False if viaje_terminado_cerca(row["pos_init"], row.pos_fin) else True, axis=1)
```
Con esto podrías filtrar las nuevas filas que no hayan terminado cerca (movimiento = true)
```python
df = df[df["mov"] == True]
```
---

## Pillar un valor filtrando DF con condición múltiple:
```python
valor = df[(df["columna_x"] == x) & (df["columna_x"] == y)]["columna"].iloc[0]
```

---

## Devolver fila completa con valor máximo
```python
df.loc[df['Value'].idxmax()]
```

---
