# Jupyter Notebook

## Crear Kernel
Crear kernel para poder cambiar de entorno on the fly

En el entorno virtual que quieres añadir:

```
pip install tornado ipykernel
ipython kernel install --user --name=kernelname
```

Y para borrarlo

```
jupyter kernelspec uninstall kernelname
```
