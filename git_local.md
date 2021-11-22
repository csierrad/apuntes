# Trabajando de forma local

A la hora de utilizar Git, no es necesario, aunque sí muy recomendable, enviar los cambios a la nube. Simplemente podemos llevar el control de nuestro proyecto desde nuestro propio sistema, lo que denominamos trabajar de forma local.  

## Inicializar un nuevo proyecto con Git

Si queremos inicializar un proyecto desde cero podemos utilizar el comando

```bash
git init carpeta-proyecto
```

Esto crea una carpeta vacía con el nombre carpeta-proyecto con Git.

También es posible que en un proyecto ya empezado queramos incluir Git. Para ello hay que dirigirse al directorio y ejecutar el comando

```bash
git init
```

Para comprobar que nuestro repositorio se ha inicializado correctamente podemos ejecutar el comando 

```bash
git status
```

Si la ejecución de este comando se produce en un directorio que no contiene Git nos mostrará un mensaje diciendo

```bash
fatal: not a git repository (or any of the parent directories): .git
```

Si de lo contrario lo introducimos en un directorio con Git inicializado, nos mostrará un mensaje similar al siguiente:

```bash
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

## Fases de nuestro proyecto en Git

Etapas por las que pasan los archivos de nuestro proyecto al utilizar Git:

- Working Directory
- Staging Area
- Git Repository

La carpeta en la que nosotros trabajamos es el 'Working Directory'. Todas las modificaciones de nuestros arcivos que llevemos a cabo aquí, no se verán reflejadas en nuestro repositorio.

Para ver los archivos modificados lo hcemos mediante:

```bash
git status
```

Cuando queramos subir estos archivos a nuestro repositorio hay que añadirlos al 'Staging Area' que es un área temporal donde nuestros archivos adquieren el estado de preparados.

Para esto utilizamos: 

```bash
git add nombre_del_archivo
```

No es necesario añadirlos de uno en uno, también se pueden añadir archivos de la siguiente forma

```bash
git add . 
#Añade todos los archivos del directorio actual

git add '*.js'
#Añade todos los archivos que terminen en .js

git add /folder
#Añade todos los archivos de la carpeta folder
```

En el caso de que nos hayamos equivocado y hayamos añadido algún archivo por error, se pueden eliminar mediante

```bash
git reset nombre_del_archivo
```

En este momento todavía no hemos guardado nuestros archivos, solamente le hemos indicado a Git que estos achivos están preparados para ser guardados.

Una vez hemos añadido todos los archivos y queremos guardar todos los cambios que tenemos en el 'Staging Area' hacemos un commit mediante el comando:

```bash
git commit -m "Texto explicativo del commit"

#Con el atributo -m añadimos al commit un mensaje que describe de forma breve el contenido del commit
```

A partir de aquí nuestros cambios están grabados en nuestro repositorio local.

Una forma de hacer commits saltandonos el área de staging es meidante la instrucción

```bash
git commit -a -m "Texto explicativo del commit"
#Este comando se puede abreviar juntando los atribuos a y m:
git commit -am "Texto explicativo del commit"
```

De esta forma Git nos añade automáticamente todos los archivos modificados de nuestro repositorio al Satagging Area y hace directamente commit de estos. Sin embargo, esto no funciona con los archivos creados que hay que añadirlos manualmente.

En el caso de que queramos deshacer el último commit podemos hacerlo de dos formas:

- Manteniendo los cambios:
    
    ```bash
    git reset --soft HEAD~1
    #El parámetro soft hace que los cambios guardados en el ultimo commit, en lugar de eliminarlos, los guarde como cambios locales.
    #El parámetro HEAD~1 indica que queremos volver al commit anterior al que nos encontramos actualmente.
    ```
    
- Sin mantener los cambios:
    
    ```bash
    git reset --hard HEAD~1
    #Elimina los últimos cambios guardados en el commit anterior
    ```
    

Para realizar cambios en el último commit pero sin eliminarlo, simplemente modificarlo, utilizmos: 

- Para arreglar el mensaje del commit anterior:
    
    ```bash
    git commit --amend -m "Mensaje nuevo del commit"
    ```
    
- Para añadir más cambios al commit:
    
    ```bash
    git add archivo_modificado.js
    #Volvemos a añadir los archivos con los nuevos cambios a añadir
    git commit --amend -m "Mensaje del commit"
    ```
    

Estas intrucciones no crean un nuevo commit sino que modifican el commit anterior. 

Sin embargo esto solamente sirve siempre y cuando los cambios no esten publicados en el repositorios remoto

## Ignorar archivos

A veces tenemos en nuestro directorio de trabajo archivos que no queremos que figuren en nuestro repositorio, como por ejemplo archivos de configuración, archivos con credenciales, dependencias ...

Para que Git no los tengan en cuenta, hay que añadirlos a un archivo .gitignore

(La siguiente [web](https://www.toptal.com/developers/gitignore) te crea un archivo .gitignore general a partir de unos parámetros como el sistema operativo, IDE, lenguaje que estamos utilizando, ...) 

## Ramas

Hasta ahora hemos trabajado en repositorios locales de forma lineal, pero Git nos ofrece la posibilidad de crear ramas para trabajar de forma paralela a nuestra rama principal. Es decir, podemos ir desarrollando nuestro proyecto y en el momento que queramos añadir una nueva funcionalidad, la desarrollamos en otra rama al margen de la rama principal y cuando la queramos incluir definitivamente, fusionamos la rama secundaria con la principal .

Para crear una rama utilizamos:

```bash
git branch nombre_de_la_rama

#Para ver las ramas que estan disponibles en nuestro repositorio local:
git branch
```

Una vez tenemos la rama creada, lo que queremos hacer es movernos de la rama principal a la rama recién creada:

```bash
git switch nombre_de_la_rama

#Para crear una rama y moverse a esta directamente:

git switch -c nombre_de_la_rama
```

### Fusionar ramas .....

(Por hacer)

### Eliminar ramas

Una vez fusionada una rama con la rama principal (aunque también puede ser con otra rama secuandaria) puede que te interese eliminar esta rama, para esto utilizamos:

```bash
git branch --delete nombre_de_la_rama
#De forma abreviada se puede escribir como:
git branch -d nombre_de_la_rama
```

Es posible que trabajando en un proyecto con varias personas, alguien fuisone una rama del repositorio remoto. A nosotros nos interesa que una vez fusionada una rama en remoto, esta desaparezca también de nuestro repositorio local. Para ello utilizamos:

```bash
git remote prune origin
#prune es un termino en ingles que significa podar (cosa que explica bastante bien el comando)

#Un atributo muy útil para el comando anterior es --dry-run
git remote prune origin --dry-run
#Esto nos permite ver antes de borrar ninguna rama, aquellas que serían eliminadas.
```
