# Makefile y la herramienta make

Indangando en distintos repositorios de Github por cosas nuevas que aprender, me percate de la existencia de unos archivos llamados Makefile que contenían una serie de instrucciones bastante raras y que no llegaba a comprender muy bien y puesto que tras investigar un poco y darme cuenta de que al final no eran cosas tran extrañas, me dispongo a realizar una serie de apuntes para que el próximo que se encuentre en esta tesitura lo tengo un poco más fácil. 

## ¿Qué es un Makefile?

A la hora de realizar un programa nos podemos encontrar en 2 situaciones: 

- Es un programa nuevo y lo tenemos que compilar por primera vez
- Hay una compilación previa, pero hemos realizado cambios en algún fichero por lo que es necesario recompilar el proyecto

Ambos casos se solucionan recompilando el código al completo, pero esta solución no es viable si se trata de proyectos de mayor tamaño. 

Para solucionar este problema surge la utilidad make y los archivos Makefile que nos permiten a la hora de recompilar un código, generar el nuevo archivo ejecutable recompilando solamente los archivos que han sufrido cambios Esto evita el recompilar archivos que ya han sido compilados previamente.

## Sintaxis del Makefile

Un Makefile es básicamente una serie de reglas que generalmente tienen la siguiente forma: 

```makefile
targets: prerequisites
	command	
	command
	command
```

- Los *targets* son nombres de archivos separados por espacios. Normalmente solo hay uno por regla
- Los *command* son los pasos que hay que llevar a cabo para hacer los archivos *target.* Las ordenes que se indiquen tiene que estar obligatoriamente tabuladas (no sirve colocar espacios en su lugar)
- Los *prerequisites* son también nombres de archivos separados por espacios. Estos son los  archivos que tienen que existir antes de que se ejecuten los *commands* para crear los archivos *target.* También reciben el nombre de dependencias.

Ejemplo sencillo de Makefile: 

```makefile
blah: blah.o
	cc blah.o -o blah # Runs third

blah.o: blah.c
	cc -c blah.c -o blah.o # Runs second

blah.c:
	echo "int main() { return 0; }" > blah.c # Runs first
```

El Makefile anterior consta de 3 reglas separadas. Al introducir en al consola *make blah* el programa nos creará el archivo blah siguiendo estos pasos:

- Como le hemo dicho que queremos crear blah, buscará blah entre todos los target.
- Para crear blah hace falta blah.opor lo que make buscará blah.o entre los target
- blah.o requiere de blah.c para su creación, buscará blah.c entre los target
- Como blach.c no requiere de ninguna dependencia, se ejecuta el comando echo creando blah.c
- Puesto que las dependencias de blah.o ya están terminadas, se ejecuta el comando    cc -c
- Por último el comando cc de la segunda fila se ejecuta ya que todas las dependencias de blah han terminado
- Como resultado tendríamos nuestro programa blah compilado

Este sería el proceso que se llevaría a cabo si se ejecuta por primera vez el Makefile y ninguna de las dependencias existe previamente. Pero ahora imaginemosque blah.c ya está creado. Al llegar a la segunda regla, el programa busca blah.c y como ve que ya existe ese archivo con ese nombre, la tercera regla no se ejecutaría.

Normalmente se suele añadir una regla llamada *clean* que se usa para eliminar el output de otros targets. Trasladandolo al ejemplo anterior, si una vez generado el archivo *blah* solamente nos interesa conservar el propio archivo *blah* y *blah.c*, solamente tendríamos que añadir al Makefile la sigueinte regla y al llamar a *make clean* blah.o sería eliminado: 

```makefile
clean: 
	rm -f blah.o
```

## Variables

LAs variables solamente pueden ser de tipo string. Normalmente se usa := , pero = también funciona (hay difenrecia entre ellos que se verá más aelante).

Ejemplo del uso de variables: 

```makefile
files := file1 file2
some_file: $(files)
	echo "Look at this variable: " $(files)
	touch some_file
```

Para hacer referencia a las variables se puede usar tanto $( ) como ${ }.

## Targets

### El target *all*

En el caso en el que tengamos diferentes targets y queramos que todos ellos se ejecuten utilizamos el target *all.*

```makefile
all: one two three

one:
	touch one
two:
	touch two
three:
	touch three

clean:
	rm -f one two three
```

### *Targets* multiples

Cuando hay más de un target para la misma regla, los comandos se ejecutan una vez para cada target.

$@ es una variable automática que contiene el nombre del target.

```makefile
all: f1.o f2.o

f1.o f2.o:
	echo $@
# Es equivalente a :
# f1.o
#	 echo $@
# f2.o
#	 echo $@
```

## Variables automáticas y wildcards(comodines)

### Wildcard *

Tanto “ * ” como “ % ” son carácteres que se utilizan como comodines en make, pero significan cosas distintas. 

‘ * ’ busca en tu sistema de archvivos por un nombre que conincida. Es recomendable que siempre lo utilicemos mediante la función wildcard porque de la otra forma caeremos en un error muy común descrito más abajo.

```makefile
# Print out file information about every .c file
print: $(wildcard *.c)
	ls -la  $?
```

‘ * ’ puede ser usado en los targets, en lso prerequisites o en la función wildcard.

Peligro: ‘ * ’ no debería ser utilizado directamente en la definición de una variable. 

Cuando esta función no encuentra ningún archivo, se queda tal y como está (a no ser que se ejecute en la función wildacard)

```makefile
thing_wrong := *.o # Don't do this! '*' will not get expanded
thing_right := $(wildcard *.o)

all: one two three four

# Fails, because $(thing_wrong) is the string "*.o"
one: $(thing_wrong)

# Stays as *.o if there are no files that match this pattern :(
two: *.o 

# Works as you would expect! In this case, it does nothing.
three: $(thing_right)

# Same as rule three
four: $(wildcard *.o)
```

### Wildcard %

% es muy útil, pero es un poco confuso debido a la multitude de situaciones en las que se puede usar.

- Cuando se usa en modo “matching”, busca coincidor con uno o más carácteres en una cadena de texto. Esta conincidencia se llama stem.
- Cuando se utiliza en modo de “reemplazo”, se sustituye a si mismo por el stem encontrado anteriormente
- Normalmente se usa en la definición de reglas y en alguna función específica.

Puesto que lo anterior puede ser un poco lioso de primeras, lo expondremos en un ejemplo:

```makefile
%.o: %.c
	#Comando a ejecutar

#Si nuestro archivo se llamase foo.c, la regla anterior sería equivalente a:
foo.o: foo.c
	#Comando a ejecutar
```

Es decir, el % toma como valor los carácteres que coinciden en los prerequisitos y los sustituye en los targets

Para más ejemplos ver las secciones: 

- Reglas de patrones estáticos
- Reglas de patrones
- Sustitución de cadenas
- La directriz????????? vpath

### Variables automáticas

Hay muchas variables automáticas, pero las más utilizadas son:

```makefile
hey: one two
	# Outputs "hey", since this is the first target
	echo $@

	# Outputs all prerequisites newer than the target
	echo $?

	# Outputs all prerequisites
	echo $^

	touch hey

one:
	touch one

two:
	touch two

clean:
	rm -f hey one two
```

## Reglas varias

### Reglas implicitas