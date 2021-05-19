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
