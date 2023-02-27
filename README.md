# **GIT**

- Software controlador de versiones.
- Interfaces Graficas:
  - Source Tree
  - GitHub Desktop
  - GitKraken
  - Visual Studio Code
- Plataformas que trabajan con Git:
  - GitHub
  - GitLab
  - BitBucket

## **Configuración Inicial**

Trabajando desde GitBash uso el comando `git --version` puedo saber que version de Git es la que tengo instalada.

Debo hacer la configuración global:

```markdown
# Configurar el usuario

git config --global user.name "Nombre de Usuario"

# Configurar el mail siendo el mismo que el de la cuenta de GitHub

git config --global user.email emaildeusuario

# Activar los colores en la ui de la terminal

git config --global user.ui true

# Mostrar la configuración de Git

git config --list

# Hacer que VS Code se vuelva el editor para configurar archivos

git config --global core.editor "code --wait"

# Hacer una edición a la configuración global desde el editor seleccionado

git config --global -e

# Estandarizar los saltos de linea en Windows

git config --global core.autocrlf true

# Estandarizas los saltos de line en Linux o Mac

git config --global core.autocrlf input

# Ver todas las opciones de la configuración en la terminal

git config -h

# Ver todas las opciones de la configuración en el navegador

git help config
```

Con `--global` configuras el Git para todas las carpetas del sistema operativo.

## **Inicializar Git en directorio local**

Debemos crear un archivo "README.md" y un archivo ".gitignore".

Para que la carpeta donde se encuentran estos archivos ya empiece a ser trakeada, debo usar el codigo `git init`. Este creara una carpeta oculta ".git" donde irá trakeando los procesos.

Y por ultimo vamos a usar "`code .`" para poder seguir trabajando desde el editor de codigo VS Code.

## **Flujo Básico**

Consta de cuatro estados, tres locales y uno remoto. Estos estados son **_modified_**, **_staged_**, **_committed_** y **_remote_**. Cada uno de ellos corresponde a un área de trabajo:

1. **_Working Directory_**: Corresponde al estado **_modified_** y es la carpeta local de tu computadora donde almacenas los archivos del proyecto.

2. **_Staging Area_**: Corresponde al estado **_staged_**, tambien llamada **_index_** porque es el área donde _git_ indexa, y agrega los cambios realizados en los archivos previos a comprometerlos en su registro.

3. **_Local Repository_**: Corresponde al estado **_committed_**, donde los cambios ya se han registrado en el repositorio de _git_. Tambien se le llama **_HEAD_** porque indica en qué cambio se encuentra el puntero del reporitorio.

4. **_Remote Repository_**: Corresponde al estado **_remote_** y es el directorio remoto donde almacenamos los archivos del proyecto el alguna plataforma _web_. _Git_ denomina **_origin_** al repositorio remoto.

![Flujo básico de Git & GitHub](https://jonmircha.com/img/blog/git-flow.png)

Para agregar los cambios de un archivo al **_staged_** debo utilizar el comando:

`git add archivo/directorio`

En caso de que quiera agragar todos los cambio de todos los archivos al **_staged_** entonces:

`git add .`

Para que los archivos sean comprometidos en el repositorio debo utilizar el comando:

`git commit`

Se abrirá el editor de codigo asignado anteriormente y en su primera linea deberás escribir el mensaje del cambio.

Hay un shortcut del comando anterios que nos permite hacer esto mismo pero sin la necesidad de abrir el editor de texto. Este sería:

`git commit -m "mensaje descriptivo del cambio`

Para agregar el origen remoto de el repositorio de GitHub utilizare el comando:

`git remote add origin https://github.com/usuario/repositorio.git`

Este mismo comando te lo dará GitHub cuando crees un repositorio en la pagina con el correspondiente usuario y nombre del repositorio.

La primera vez que vinculamos el repositorio remoto con el local debemos utilizar el comando:

`git push -u origin master`

Para las siguientes actualizaciones, si no hay cambios de rama, utilizaras simplemente:

`git push`

Si quiero descargar todos los cambios realizas desde GitHub utilizo:

`git pull`

## **De _master_ a _main_**

### Para repositorios nuevos

Si voy a crear nuevos repositorio voy a cambiar ya desde el inicio _master_ por _main_. Para ello utilizare:

```
git init
git add .
git commit -m "Primer commit"
git branch -M main
git remote add origin https://github.com/usuario/repositorio.git
git push -u origin main
```

### Para repositorios existentes

Utilizaremos los siguientes comandos:

```
git branch -M main
git remote add origin https://github.com/usuario/repositorio.git
git push -u origin main
```

### Para reemplazar la rama _master_ por _main_

Para remplazar la rama _master_ por _main_ en GitHub debo usar los siguientes pasos:

1. `git branch -m master main`

2. `git push -u origin main`

3. `git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main`

4. Debo cambiar la rama _default_ de _master_ a _main_ en el repositorio GitHub.
   Para eso voy a _settings_ en el repositorio, voy a la opcion _branches_ y cambio la nueva rama por default de _master_ a _main_.

5. `git push origin --delete master`

## **Ayuda**

Si necesito ayuda para los comando de _git_ puedo usar los siguientes codigos en la terminal:

- Para ayuda desde la terminal:

  `git nombrecomando -h`

- Para ayuda desde el navegador:

  `git help nombrecomando`

## **Ignorar Archivos**

En el archivo _gitignore_ incluimos todo lo que **NO** queramos incluir en nuestro repositorio.

Si son archivos o carpetas especificas, unicamente tengo que poner su nombre

```
archivo.ext
carpeta
/archivo_desde_raiz.ext
```

Si tengo que ignorar todos los archivos con un tipo de extension:

```
\*.ext
```

Y si quiero que sean todos excepto alguno en particular uso:

```
!.ext
```

Para ignorar archivos ciertos archivos dentro de una carpeta pongo la ubicacion y lo que quiero ignorar:

```
doc/\*.txt
```

En caso de que haya subcarpetas las cuales tambien queres ignorarlas, utilizo:

```
doc/\*_/_.txt
```

## **Clonar Repositorio**

Si quiero clonar un repositorio, no importa de quien sea, simplemente tengo que escribir el comando:

```

git clone urldelrepositorio.git

```

En _GitHub_ ya te da la opcion de copiar la URL junto con _.git_ al final de la misma.

## **Ramas**

Una rama nos permite aislar una funcionalidad del codigo. Sirve para crear codigos paralelos al codigo _main_ y luego añadirlos a codigo principal.

```markdown
# crear rama

git branch nombre-rama

# cambiar de rama

git checkout nombre-rama

# crear una rama y cambiarte a ella

git checkout -b rama

# eliminar rama

git branch -d nombre-rama

# forzar eliminar rama

git branch -D nombre-rama

# listar todas las ramas del repositorio

git branch

# listar ramas no fusionadas a la rama actual

git branch --no-merged

# lista ramas fusionadas a la rama actual

git branch --merged

# rebasar ramas

git checkout rama-secundaria
git rebase rama-principal
```

## Fusiones

Las fusiones se usan para unir dos ramas. Para ello debo encontrarme en la rama a la cual se le van a fusionar las ramas indicadas.

Hay dos tipos de fusiones:

- _**Fast-Forward**_: La fusión se hace automaticamente y no hay problemas resultantes.

- _**Manual Merge**_: En este caso la fusión se hará manualmente ya que se encontraron problemas con duplicación de archivos.

Los comandos para fusionar son:

```markdown
# Hacer cambio a la rama principal donde se hará la fusión

git checkout rama-principal

# Ejecutar el comando de fusión con la rama que se va a fusionar con la principal.

git merge rama-secundaria
```

En el caso de que la fusión sea _**Manual Merge**_ hay que resolver los problemas de duplicados seleccionando que es lo que quede en el archivo.

## Cambios

Se pueden modificar los ultimos cambios realizados.

```markdown
# Agrega los cambios sin editar el mensaje del ultimo commit

git commit --amend --no-edit

# Edita el mensaje del ultimo commit

git commit --amend -m "Nuevo mensaje para el último commit"

# Elimina el ultimo commit

git reser --hard HEAD~1
```

Podemos viajar entre el historial del repositorio sin afectar el repositorio como tal.

```
git checkout id-commit
```

Para saber el _id-commit_ utilizo el comando `git log --oneline` y podre ver el historial de commits realizados.

**_MUY IMPORTANTE!!!_**

El realizar cambios despues de hacer un _push_ va a provocar conflictos los cuales tendremos que resolver de forma manual y luego crear un nuevo _commit_ con esos problemas resueltos.

## Registo del historial

El comando `git log` nos permite conocer todo el historial de un proyecto.

```markdown
# Mostrar en una sola línea

git log --oneline

# Guardar el log en la ruta y archivo que especificamos

git log > commits.txt

# Mostrar el historial con el formato que indicamos

git log --pretty=format:"%h - %an, %ar : %s"

# Mostrar cierta cantidad de cambios, remplazando la n por la cantidad

git log -n

# Mostrar cambios realizados después de una fecha especificada

git log --after="2010-03-04 00:00:00"

# Mostrar cambios realizados antes de una fecha especificada

git log --before="2010-03-04 00:00:00"

# Mostrar cambios en un rango de fecha

git log --after="2010-03-04 00:00:00" --before="2010-03-04 00:00:00"

# Mostrar TODO el registro de acciones (inserciones, cambios, eliminaciones, fusiones, etc.)

git reflog

# Mostrar diferencias entre el Working Directory y el Staging Area

git diff

# Mostrar en forma de grafico los cambios realizados

git log --oneline --graph --all
```

## Reseteo del historial

Podemos eliminar el historial de cambios de un proyecto.

```markdown
# Mostrar listado de archivos nuevos, borrados o editados

git status

# Borrar HEAD

git reset --soft

# Borrar HEAD y Staging

git reset --mixed

# Borrar HEAD, Staging y Working Directory

git reset --hard

# Deshacer todos los cambios despues del commit indicado, preservando los cambios locales

git reset id-commit

# Desechar todo el historial y regresa al commit especificado

git reset --hard id-commit
```

## Resetear un repositorio

Se puede resetear el historial de cambioas de un repositorio para que quede como si lo acabarás de crear.

```markdown
# Entrar en el repositorio

cd carpeta-repositorio

# Mover el archivo de configuracion a el directorio del usuario

mv .git/config ~/saved_git_config

# Forzar la eliminación de directorio .git

rm -rf .git

# Inicializar el directorio

git init

# Añadir todos los archivos

git add .

# Añadir el nuevo primer commit

git commit -m "Primer commit"

# Restaurar el archivo de la configuración

mv ~/saved_git_config .git/config

# Forzar el push para que no haya problemas

git push --force origin main
```

Esta práctica se suele realizar par no tener tantas versiones o commits del archivo y ahorrar espacio. Es mas que nada para repositorios personales los cuales no haya problema con necesitar el historial de commits. No es recomendable hacerlo en un repositorio importante.

## Remotos

```markdown
# mostrar los origenes remotos del repositorio

git remote

# Mostrar los origenes remotos con detalle

git remote -v

# Agregar un origen remoto

git remote add nombre-origen https://github.com/usuario/repositorio.git

# Renombrar un origen remoto

git remote rename nombre-viejo nombre-nuevo

# Eliminar un origen remoto

git remote delete nombre-origen

# Descargar una rama remota a local diferente a la principal

git checkout --track -b rama-remota origin/rama-remota
```
