# Linux

### Add to PATH
Permite ejecutar programas, que estén en el directorio que añadas, desde cualquier sitio.

Editar `/home/usuario/.profile` y añadir al final

`export PATH=$PATH:/path/to/dir`

Reiniciar la terminal o ejecutar `source .profile`

### Crontabs

`crontab -l` see.

`crontab -e` edit.

`sudo crontab -u <username> -l` other user's crontab.

# Ubuntu
### Create executable for the Ubuntu UI.
Te lo encontrará el sistema y poder ejecutarlo con su icono y tal.

Crear un archivo en `/usr/share/applications` y llamarlo `mi-programa.desktop` y llenarlo por ejemplo con:

```
#!/usr/bin/env xdg-open
[Desktop Entry]
Type=Application
Name=Android Studio
Exec="/home/javi/android-studio/bin/studio.sh"
Icon=/home/javi/android-studio/bin/studio.png
Categories=Application;Programming;Android;Mobile
```
