# Plotly

## Crear figura con multiples líneas

```python
import plotly.express as px
import pandas as pd

df = pd.read_csv("data/serie_atocha_crudo.csv")
# columnas = fecha, motos_disponibles, iniciados, finalizados


fig = px.line(df, x="fecha", y=["motos_disponibles", "iniciados"],  width=2200, height=1000, title="layout.hovermode='x'")
fig.update_layout(hovermode="x") # para que al pasar el cursor te muestre ambos valores
fig.show()

```

### Histogram when Y axis is already computed
Use ```px.bar()```

```px.histogram()``` won´t work because it will try to count the Y axis again lmao.

```
          fecha                   finalizados
0	2021-10-06 00:00:00	  2
1	2021-10-07 00:00:00	  39
2	2021-10-08 00:00:00	  63
3	2021-10-09 00:00:00	  44
4	2021-10-10 00:00:00	  60
```

```python
fig = px.bar(finalizados_dias_df, x="fecha", y="finalizados")
fig.show()
```
