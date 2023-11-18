# Apunte sobre GIT

*Aviso:* Contiene faltas de ortografia.

Esto no es un *cheat-sheet* son notas a modo de apunte que escribi mientras aprendia Git.

## Configuración
La configuracion mas basico de git es nuestro nombre y correo electronico.

```
git config --global user.name "CiroMirkin"
```

```
git config --global user.email ciromirkin@gmail.com
```

Entrega la lista de configuraciones

```
git config -h
```

### configuraciones de editor

Establece al editor por defecto

```
git config --global core.editor "code --wait"
```

Abre el archivo de configuracion

```
git config --global -e
```

Configuracion de espacios

```
git config --global core.autocrlf true
```

*inut* si estas en mac

## Añadir archivos

Estas son las formas que mas usaras para añadir archivos.

```
git add file.txt
git add file1.txt file2.txt
git add *.txt
```

Y luego tenemos esta forma que es considerada una mala practica, por agregar cosa que puede ser inecesarias como lo pueden ser las imagenes.

```
git add . 
```

**Recuerda que:** No se agregan los archivos sino sus cambios y/o modificaciones

## git commit

La forma mas rapida para crear un commit con una descripcion breve es esta:

```
git add .
```

```
git commit -m "Commit inicial"
```

Y luego tenemos la tradicional, para descripciones mas largas.

```
git commit
```

## git rm (Eliminar archivos)

Usualmente lo ariamos asi:

```
rm file2.txt
git add file2.txt
git commit -m "Eliminando archivo 2"
```

Pero es meyor hacerlo asi:

```
git rm file2.txt
```

## git restore (Restaurar cambios y/o archivos)

Para restaurar cambios:

```
git restore --staged file.txt
```

Para restaurar archivos.

```
git restore file.txt
```

## git mv (Cambiar el nombre de un archivo)

Usualmente lo hariamos asi:

```
mv file1.txt file.txt
```

Pero es mejor asi:

```
git mv file1.txt file.txt 
```


## .gitignore

Creamos el archivo .gitignore

Y luego un commit

```
git add .gitignore
git commit -m "agregando archivo gitignore"
```

## Git status

Podemos ver el estado de los archivos asi:

```
git status
```

O asi con menos informacion:

```
git status -s 
```

Donde:

> M (Modificado)
> A (Agregando)
> ?? (No agregado)

## git diff

Nos muestra los cambios que serian agregados y los antiguos

```
git diff
```

> u (para salir

Nos muestra los cambio agregados

```
git diff --staged 
```

## git log

Todos los commit en una linea sin info extra

```
git log --oneline
```

> q - Para salir

Vemos los cambios hechos en tamaño

```
git log --stat
```

## Tag

### Crear un tag

```
git tag -a v0.1 -m "Descricion del tag" ch
```

En el lugar del *ch* va el hash del commit donde estara el *tag*

El *v0.1* es el nombre del tag, al usarce para marcar verciones suele ser asi por convencion.


### Ver los tags

Para ver solo los nombres

```
git tag
```

Para ver los nombre y el hash del commit donde estan

```
git show-ref --tags
```

### Subir tags a GitHub

```
git push origin --tags
```

### Eliminar tags

**Forma superficial**, desaparece de git pero no de GitHub

```
git tag -d nombre
```

En este caso el *nombre* podria ser *v0.1*

**Forma profunda**, desaparece de git y de GitHub

```
git tag -d nombre
```

Y luego

```
git push origin :refs/tags/nombre
```

## git reset

Con este comando volvemos hacia atras sin posibilidad de revertir esta ida hacia atras.

*ch* aqui va el hash del commit al que queremos volver

```
git reset ch --soft
```

Volvemos a este commit perdiendo todos los cambios anteriores a este commit

```
git reset ch --hard
```

Para eliminar el ultimo commit sin borrar los cambios solo el commit, generalmente para volver a hacer el commit porque  cometimos un error en la descripcion.

```
git reset HEAD~1
```

## git checkout

Mas alla de poder cambiar de rama podemos:

Hacer que un archivo regrese al estado en el que estaba en cierto commit.

```
git checkout ch main.py
```

*ch* commit hash

Luego de ejecutar este comado podemos hacer cambios y un commit, o simplemente hacer un commit para registrar este nuevo estado.

```
git add .
git commit -m ""
```

**Para revertir** antes de hacer el commit, osea volver al ultimo commit que hicimos

```
git checkout master main.py
```

## Pull requeste (PR)

Esta es una caracteristica de GitHub.

Pasos que se suelen seguir en git:


```
git swich -c newFeatureName
git push origin newFeatureName
```

Agregamos lo que tengamos que agregar en la nueva rama

```
git commit -am ""
git push origin newFeatureName
```

Ahora en GitHub hacemos la respectiva PR.