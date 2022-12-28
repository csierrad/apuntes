Fuente -> https://www.sciencedirect.com/topics/engineering/floating-point-number

Los floating-point numbers son análogos a los números representados en notación científica. Como en la notación científica, los floating-point numbers constan de 4 partes, el signo, la mantissa, la base y el exponente. Por ejemplo 4.1 x 10³ es número representado en notación científica en el que el signo sería +, la mantissa 4.1, la base sería 10 y el exponente 3. En el caso de los número binarios en coma flotante, cambia la base que sería 2 y por consiguiente el resto de números. 
Por ejemplo vamos a representar en coma flotante el número de 228 en una variable de 32 bits. Esos 32 bits, se dividen en 3 partes, **el bit significativo** que es el primero empezando por la izquierda, **el exponente** que se representa con 8 bits y **la mantissa** que se representa con 23 bits quedando los 32 bits distribuidos de la siguiente manera: 
				SEEE EEEE	EMMM MMMM	MMMM MMMM	MMMM MMMM
				S: Bit significativo
				E: Exponente
				M: Mantissa

Lo primero es convertir el número en base 10 a base decimal
	228(10) = 111001100 (2) = 1.11001 (2) x 2⁷

>NOTA: Al final la única diferencia entre los números en base 10 y 2 es la base y el comportamiento con los decimales es el mismo, es decir, si a un número en base decimal lo dividimos por 10², la coma se mueve 2 espacios a la izquierda y pasa lo mismo con los números binarios, si divides por 2² se moverá la coma 2 espacios a la izquierda.

En nuestro ejemplo, el bit significativo sería 0 (es un número positivo), el exponente 7 y la mantissa 1.11001. 
Como se puede observar, el primero bit de la mantissa siempre será un 1 por lo que por optimización, este bit no se guarda. Dicho esto, nos quedaría como resultado el siguiente número:
		0	00000111	110 0100 0000 0000 0000 0000
		
Por último es necesario hacer un cambio al exponente con el objetivo de poder disponer tanto de exponentes positivos como negativos. Para esto lo que hacemos es sumar una constante al exponente, que en este caso es 127. 
En nuestro ejemplo el exponente al tener el valor 7, se convertiría en el 134 y si por ejemplo hubiese sido el -2, habría tomado el valor de 125.
inalmente nos queda como resultado el siguiente número:
		0	10000110	110 0100 0000 0000 0000 0000
		
		
Para pasar de binario a decimal, lo único que habría que hacer es:
	- Hallar el valor que tiene el exponente y restarle 127
	- Añadir el 1 a la mantissa que anteriormente hemos quitado
	- Mover la coma de la mantissa tantos espacios como indique el exponente
	- Calcular el número con las potencias de 2 teniendo en cuenta que a partir de la coma, las potencias de 2 son negativas. Por ejemplo, el número 1.101 sería el resultado de la suma de 2⁰ + 2⁻¹ + 2⁻³
	- Y por último tener en cuenta el signo del bit significativo