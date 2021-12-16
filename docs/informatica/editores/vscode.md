# VSCode


## Comando abrir acciones

Ctrl + shift + p


## Workspace
Para tener abiertos distintos repos a la vez y no reiniciar el VSCode

Crear archivo `nombre_cualquiera.code-workspace` con 

```
{
   "folders":[
      {
         "name":"nombre_repo_1",
         "path":"realitve/path/to/repo_1"
      },
      {
         "name":"nombre_repo_2",
         "path":"realitve/path/to/repo_2"
      },
   ]
}

```
## Cursor movement
- Go back to previous loc: `Ctrl Alt -`
- Go forward loc: `Ctrl Shift -`

### VIM VSCode
- Go beggining of file: `gg`
- Go end of file: `G`
- Replace stuff, use \ to scape special characters

`:%s/foo/bar/g`

- Select word under cursor: `viw`

#### Cursor:
- Go to function definition: `ctr+]`
- Go back: `ctrl+o`
- Go forth: `ctrl+i`

