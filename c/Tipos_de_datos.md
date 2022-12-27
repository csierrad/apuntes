# Tipos de datos

Los tipos de datos en C se pueden clasificar de la siguiente manera:
	- Tipos básicos: son tipos aritméticos y se pueden clasificar a su vez en enteros o en tipos de coma flotante.
	- Enumereted types: son también tipos aritméticos y se usan para definir varaibles que solamente pueden tomar determinados valores durante el flujo del programa
	- Void type: `el tipo void indica que no hay un valor disponible`
	- Derived types: dnde se incluyen los punteros, los arrays, las estructuras, las uniones y las funciones 

## Valores enteros
Pueden ser:
	- **char** (1 byte) -> valores: desde -128 hasta 127 o de 0 hasta 255
		- unsigend char (1 byte) -> valores: entre 0 y 255
		- signed char (1 byte) -> valores: entre -128 y 127 
	- **int** (2 o 4 bytes) -> valores: entre -32,768 y 32,767 o desde -2,147,483,648 hasta 2,147,483,647
		- unsigned int (2 o 4 bytes) -> valores: entre 0 y 65,535 o entre 0 y 4,294,967,295
	- **short** (2 bytes) -> valores: entre -32,768 y 32,767
		- unsigned short (2 bytes) -> valores: entre 0 to 65,535
	- **long** (8 bytes) -> valores: desde -9,223,372,036,854,775,808 hasta 9,223,372,036,854,775,807
		- unsigned long (8 bytes) -> valores: desde 0 y 18,446,744,073,709,551,615


> NOTA: En el estándar de C no se especifíca si char es signed o unsigned por defecto, solamente se indica el tamaño que debe tener (1 byte), por lo que depende de cada compilador (en gcc se trata como signed). Es por eso que hay dos rangos de valores para char dependiendo de si es tratado como signed o unsigned

> NOTA: actualmente las variables int suelen ocupar 4 bytes pero en los compiladores más antiguos solían tener 2. El estándar de C solamente indica que una variable de tipo int podrá almacenar como mínimo valores entre -32767 y 32767 para lo que se requieren 16 bits, pero los propios compiladores pueden superar ese límite. ara saber que tamaño utiliza nuestro compilador lo mejor es utilizar la función sizeof().


## Floating-Point Types.
Son un conjunto de data types que no se comportan de la misma manera que los indicados anteriormente. Mientras que en los tipos enteros se guarda el valor que tiene la variable tal cual (en binario), los tipos que se representan mediante coma flotante se comportan distinto -> [Explicación de la coma flotante](./Representacion_de_decimales_con_coma_flotante)

- float (4 bytes) -> 
	- valores: 1.2E-38 to 3.4E+38
	- precisión: 6 decimales
- double (8 bytes) -> 
	- valores: 2.3E-308 to 1.7E+308
	- precision: 15 decimales
- long double (16 bytes) ->
	- valores: 3.4E-4932 to 1.1E+4932
	- preciosion: 19 decimales
