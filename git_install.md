# Instalación y configuración

## Descarga de GIT

Para saber si tenemos instalado GIT en nuestro sistema corremos el comando

```bash
git --version
```

Si nos devuelve como resultado la versión disponible en nuestro sistema, significa que está disponible, de lo contrario, si nos indica el siguiente mensaje:

```bash
command not found: git 
```

tendremos que instalarlo mediante el comando

```bash
apt-get install git
```

## Configuraciones iniciales:

Configuración del nombre:

```bash
git config --global user.name "nombre"
```

Configuración del correo:

```bash
git config --global user.email "tu correo"
```

Configuración del editor por defecto:

```bash
#(para que sea VSC)
git config --global core.editor "code"
```

Configuración del nombre de la rama inicial de nuestros proyectos:

```bash
git config --global init.defaultBranch <nombre>
```

Por defecto el nombre de la rama principal es 'master', un termino que poco a poco se está sustituyendo por otros como 'main'.

Todas las caracteristicas anteriores se pueden modificar solamente para un repositorio en concreto. Para esto lo único que hay que hacer es quitar el atributo --global

En el caso de que queramos comprobar la configuración que estamos utilizando, utilizamos:

```bash
git config --list
```

Puesto que podemos tener varios archivos gitconfig en nuestro sistema (puede existir uno de configuración local, otro de configuración global y otro de configuración del sistema) el comando anterior puede darnos resultados repetidos, ante lo cual tenemos que saber que el que prevalece es el último.

```bash
git config --global --list
```

Para poder visualizar solamente el gitconfig que nos interese, podemos utilizar los argumentos 

--global, --local y --system.

```bash
git config --global --list   (Nos muestra la configuración global de git)
```

Otra forma de ver esto es mediante el atributo --show-scope que nos muestra delante de cada elemento a que configuración pertenece

```bash
git config --list --show-scope
```

(Si este último comando no funciona prueba a actualiazar a la última versión de GIT disponible)

Por último si queremos saber solamente un elemeto de la configuración determinado utilizamos

```bash
git config <configuración> 
#Por ejemplo: 
# git config user.mail
```