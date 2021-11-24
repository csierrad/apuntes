# Trabajando de forma remota

Por ahora todo el registro de nuestro proyecto lo hemos almacenado en nuetro ordenador, cosa que para proyectos individuales puede tener sentido, pero la verdadera utilidad de Git es poder compartir esos cambios con un equipo de trabajo de manera remota.
Para esta tarea, una de las herramientas más utilizadas es GitHub.

## Creando un repositorio remoto en GitHub

Crear un repositorio en GitHub es totalmente gratis pero es necesario estar registrado. Para ello solamente tienes que dirigirte a la página de [GitHub](https://github.com/) y crear una cuenta nueva. 

Una vez creada aparecerá arriba a la derecha un simbolo de + que nos sirve para varias cosas, entre las que está crear un repositorio. Una vez pulsemos este botón nos aparecerá una ventana en la que tras rellenar una serie de campos nos permitirá crear nuestro repositorio.

## Clonando un repositorio remoto ya creado

Es posible que queramos trabajar en un repositorio que ya se ha creado anteriormente. Para esto utilizaremos la herramienta clonar de Git. 

Para poder hacer esto necesitamos saber la dirección de de dicho repositorio, que puede ser tanto una dirección HTTPS o SSH. Por lo general es preferible utilizar SSH.

Para encontrar esta dirección solamente hay que dirigirse a un repositorio cualquiera de GitHub y arriba a la derecha aparecerá un botón verde con la palabra Code. Pinchando se abrirá un desplegable en el cual encontramos ambas claves. 

Una vez tengamos la dirección SSH el comando a utilizar es:

```bash
git clone dirección_SSH_del_repositorio

# Por defecto esto nos crea una carpeta con el mismo nombre que tenía originalmente, pero si queremos cambiarlo
# solamente hace falta añadir un atributo más a la instrucción indicando el nombre nuevo de la carpeta

git clone dirección_SSH_del_repositorio nombre_nuevo
```

Esto crea una copia en el directorio actual tanto de los archivos de los que se compone el repositorio como de los commits y ramas utilizados para llegar a esa versión del proyecto.

## Enlazar nuestro repositorio local con uno remoto

Para enlazar nuestro repositorio local con uno remoto se hace mediante la instrucción

```bash
git remote add alias_repositorio dirección_repositorio

# alias_repositorio - nombre que tendrá nuestro repositorio remoto en nuestro ordenador. Ej: origin
# dirección_repositorio - dirección SSH o HTTPS del repositorio remoto (la misma del apartado anterior)
```

Un comando muy útil que nos permite ver los repositorios que tiene enlazados nuestro repositorio local es

```bash
git remote
# Si queremos más detalles utilizamos el parámetro -v
git remote -v
```

## Esribir en el repositorio remoto

Una vez tenemos enlazados los repositorios local y remoto, es hora de guardar en el remoto los cambios que hemos hecho en el local. Para ello utilizamos

```bash
git push alias_repositorio nombre_rama

# alias_repositorio - hace referencia al apodo que le hemos dado en el apartado anterior a nuestro
#                     repositorio remoto. Ej: origin
# nombre_rama - nombre de la rama de la que queremos enviar los cambios. Ej: main
```

# Continuará...
