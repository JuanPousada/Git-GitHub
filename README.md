# GIT

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

## Configuración Inicial

Trabajando desde GitBash uso el comando `git --version` puedo saber que version de Git es la que tengo instalada.

Debo hacer la configuración global:

- `git config --global user.name "Nombre de Usuario` - configura el usuario.
- `git config --global user.email emaildeusuario` - configura el mail. Es importante que sea el mismo con el que vamos a tener la cuenta de GitHub.
- `git config --global user.ui true` - Activa los colores en la ui de la terminal.
- `git config --list` - Nos muestra la configuracion de Git.
- `git config --global core.editor "code --wait` - Hace que Visual Studio Code se vuelva el editor para configurar archivos.
- `git config --global -e` - Es para hacer una edición a la configuración global desde el editor seleccionado.
- `git config --global core.autocrlf true` - Sirve para estandarizar los saltos de linea en Windows.
- `git config --global core.autocrlf input` - Sirve para estandarizar los saltos de linea en Linux o Mac.
- `git config -h` - Sirve para ver todas las opciones de la configuración en la terminal.
- `git help config` - Sirve para ver todas las opciones de la configuración en el navegador.

Con `--global` configuras el Git para todas las carpetas del sistema operativo.

## Inicializar Git en directorio local

Debemos crear un archivo "README.md" y un archivo ".gitignore".

Para que la carpeta donde se encuentran estos archivos ya empiece a ser trakeada, debo usar el codigo `git init`. Este creara una carpeta oculta ".git" donde irá trakeando los procesos.

Y por ultimo vamos a usar "`code .`" para poder seguir trabajando desde el editor de codigo VS Code.

## Flujo Básico

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

## De _master_ a _main_

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
