# Git

## Ramas

Crear:
`git branch nombre_rama`

Cambiar a: 
`git checkout nombre_rama`

Combinar crear y cambiar:
`git checkout -b nombre_rama`

## Merge
Mergea la rama que digas -> en la que estás `feature/feature_mazo_wapo -> develop`

`git checkout develop`

`git merge feature/feature_mazo_wapo`

## Rebase
Incluye los cambio de otra rama en la tuya, "la rebasa".

Estás en rama **feature/cosa_wapa** y has hecho algún cambio directo en la rama develop por cualquier movida o esque eres imbécil:

En la rama **feature/cosa_wapa**


          A---B---C feature/cosa_wapa
         /
    D---E---F---G develop
    
 `git rebase develop`
 
                  A'--B'--C' feature/cosa_wapa
                 /
    D---E---F---G develop
 
 jeje
 
 ## Grep
 -n muestra la linea con enlace
 
 `git grep -n "cosa_interesante"`
 
 
 ## Autorizar SSH
 
 Puede dar el error `git@github.com: Permission denied (publickey)...`
 
 Seguir los pasos de generate, add y SAML (para organización) [GitHub](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
