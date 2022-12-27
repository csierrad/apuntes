## Operadores binarios

### NOT(x) -> ~
A diferencia del resto de operadores, NOT es el único que trabaja solamente con 1 número.
El operador binario NOT cambia cada uno de los bits del número x por sus complementarios. Ejemplo:
		x 	-> 1001110
		~x -> 0110001

### AND(x, y) -> &
Da como resultado otro número como resultado de aplicar a cada posición de ambos números la condición AND, es decir, una posición n del número resultado será 1 si y solo si en la misma posición n de los números originales hay 1. Ejemplo:
		x 		->	10011100
		y 		->	11011001
		x & y ->  10011000
		
### OR(x, y) -> |
El resultado de la operación OR de dos números da un tercero cuyos bits serán 1 si alguno de los dos bits de los operandos es 1. Ejemplo:
		x 		->	10011100
		y 		->	11011001
		x | y  ->11011101

### XOR(x, y) -> ^
La operación XOR de dos números da como resultado un tercero cuyos bits serán 1 si y solo si uno de los operandos tiene un 1 en esa posición. Ejemplo:
		x 		->	10011100
		y 		->	11011001
		x ^ y ->01000101
		
		
### Operadores de desplazamiento
Hay dos operadores de desplazamiento, el >> (desplazamiento a la derecha)  y << (desplazamiento a la izquierda). Este operador toma dos números y se encarga de desplazar los bits del operando que se encuentra a la izquierda del operador el número de veces que le indica el operando de la derecha. Ejemplo:
		x			->  10011100
		x << 2 	->	01110000
		x >> 2	->	00100111
		
	
	
Los operadores anteriores nos dan una nueva forma de interactuar con las variables en la que podemos controlar cada uno de los bits individualmente. 
Esto es especialmente útil en por ejemplo a la hora de guardar muchos valores booleanos, en los que solamente necesitamos saber si es true o false, está o no está, ...
Esta tarea para la que antes se necesitava una varable entera para guardar un valor, ahora podemos en una misma variable, por ejemplo de y byte, 8 bits, guardar el valor de 8 variables booleanas asignando a cada variable diferentes bits. 
Ejemplo:
 Imaginemos que tenemos una lista de 8 colores distintos de los cuales nosotros escogemos algunos y queremos almacenar cuáles hemos elegido.
 Esto se puede hacer asignando a cada uno de los colores un bit de una variable, por ejemplo, unsigned char ya que ocupa 8 bits de memoria.
 
 ROJO				 1 0 0 0 0 0 0 0
 VERDE				0 1 0 0 0 0 0 0
 AMARILLO 		 0 0 1 0 0 0 0 0
 AZUL				  0 0 0 1 0 0 0 0 
 BLANCO			  0 0 0 0 1 0 0 0 
 NEGRO				0 0 0 0 0 1 0 0 
 MARRON			  0 0 0 0 0 0 1 0 
 NARANJA		  0 0 0 0 0 0 0 1
 
 De esta manera en una variable que llamaremos colores guardamos un valor que en binario sea el  1 1 0 0 1 0 0 1  podremos indicar que hemos elegido los colores ROJO, VERDE, BLANCO Y NARANJA.
 Pero para poder llevar esto a cabo necesitamos poder añadir y quitar 1 en la posición que queramos y poder saber si hay un 1 en una determinada posición. Para ello utilizamos los operadores que hemos visto antes.
 
 Para añadir un uno:
 
 0 0 0 0 0 0 0 0
 0 0 0 0 1 0 0 0	OR
____________
0 0 0 0 1 0 0 0


Para quitar un uno:

0 0 0 0 1 0 0 0
1  1  1 1 0 1 1  1 		AND(x, ~x)
____________
0 0 0 0 1 0 0 0


Para ver si hay un uno en alguna posición:

 1 0 0 0 1 0 1 0
 0 0 0 0 1 0 0 0	AND
____________
0 0 0 0 1 0 0 0


Esto se puede hacer con varios números al mismo tiempo y en el orden que queramos