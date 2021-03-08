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
