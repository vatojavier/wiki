# Pandas

## Pillar un valor filtrando DF con condición múltiple:

```python
valor = df[(df["columna_x"] == x) & (df["columna_x"] == y)]["columna"].iloc[0]
```
## Devolver fila completa con valor máximo

```python
df.loc[df['Value'].idxmax()]
```
