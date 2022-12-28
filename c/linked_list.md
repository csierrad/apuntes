# Linked list

[APUNTES ORIGINALES](https://www.geeksforgeeks.org/linked-list-set-1-introduction/?ref=lbp)

# SINGLY LINKED LIST

Al igual que los arrays, las `linked lists` son estructuras de datos de tipo lineal , pero a diferencia de estos, los elementos no se guardan de manera contigua en memoria, sino que se utilizan punteros para relacionar unos elementos con los otros.

## Por qué utilizar `linked list`?

Los arrays se pueden utilizar para almacenar datos del mismo tipo, pero tienen una seria de limitaciones:

- El tamaño del array es fijo por lo que tenemos que saber el tamaño máximo con anterioridad. Además, la reserva de espacio en memoria coincide con el límite máximo independientemente de si se usa o no.
- Insertar un nuevo elemento en un array es costoso ya que hay que crear espacio para los nuevos elementos y hay que de sitio los que ya existían. Pero en las `Linked Lists` tenemos un nodo inicial a través del que podemos viajar al resto de nodos y insertar o eleminar un nodo en la posición deseada.

Ventajas sobre los arrays:

- Tamaño dinámico
- Fácil inserción y eliminación de elementos

Deventajas sobre los arrays:

- No se puede acceder a elementos aleatorios. Tenemos que acceder a los elementos secuencialmente empezando desde el primero nodo.
- Se emplea mayor cantidad de memoria para guardar cada elemento ya que además del propio dato hay guardar un puntero.
- Las `Linked Lists` no son “cache friendly”.

## Representación

Una `linked list` está representado por un puntero con la dirección en memoria del primero nodo del la lista. El primero nodo se llama **Head**. Si la lista está vacía, el valor del puntero hacia **Head** es NULL.

Cada uno de los nodos de la lista consisten de al menos dos partes:

- Los **datos** que pueden ser de cualquier tipo
- El **puntero** al siguiente nodo

En C se puede representar nodos utilizando `structs`.

```c
struct Node {
    int data;
    struct Node* next;
};

//Para mejor legibilidad:

typedef struct node {
    int data;
    Node* next;
} Node;
```

## INSERTAR NODOS

Un nodo se puede introducir de 3 formas distintas:

- Al principio de la lista
- A continuación de un nodo dado
- Al final de la lista

### Añadir un nodo al principio de la lista ( push() )

El nodo nuevo hay que añadirlo antes del nodo head de la lista dada pasando a ser este último nodo añadido la referencia de head. La función que se encargará de esto se llamará **push** y recibirá como parámetros un puntero a head y el nuevo dato a introducir.

```c
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));

    new_node->data  = new_data;

    new_node->next = (*head_ref);
  
    (*head_ref)    = new_node;
}
```

### Añadir un nodo a continuacón de otro nodo dado ( insertAfter() )

Como parámetro la función recibirá un puntero al nodo previo y los datos a añadir.

 

```c
void insertAfter(struct Node* prev_node, int new_data)
{
    if (prev_node == NULL) {
        printf("the given previous node cannot be NULL");
        return;
    }
 
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));
 
    new_node->data = new_data;
    new_node->next = prev_node->next;

    prev_node->next = new_node;
}
```

### Añadir un nodo al final de la lista ( append() )

Como una Linked List está generalmente representado por el nodo head, será necesario atravesar la lista hasta el final y cambiar la variable next del ultimo nodo de NULL al nuevo nodo añadido.

```c
void append(struct Node** head_ref, int new_data)
{
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
 
    struct Node *last = *head_ref;
  
    new_node->data  = new_data;

    new_node->next = NULL;
 
	  /* Si no hay nodos en la lista */
    if (*head_ref == NULL)
    {
       *head_ref = new_node;
       return;
    } 

    while (last->next != NULL)
        last = last->next;

    last->next = new_node;
    return;   
}
```

## ELIMINAR NODOS

A la hora de eliminar un nodo podemos hacerlo en función de:

- El valor que contiene el nodo
- La posición del nodo

### Elminar un nodo en función de su valor

Antes de nada formulemos la tarea a llevar a cabo a la hora de eliminar un nodo. 

“*Dado un determinado valor, eliminar la primera acurrencia de dicho valor en la lista.”*

Esta taresa se puede realizar de dos formas distintas:

- **Método iterativo:**
    
    Para eliminar un nodo de la lista tenemos que seguir los siguientes pasos:
    
    - Encontrar el nodo anterior al que queremos eliminar
    - Cambiar el puntero *next* del nodo anterior
    - Liberar la memoria del nodo eliminado.
    

```c
/* Given a reference (pointer to pointer) to the head of a
list and a key, deletes the first occurrence of key in
linked list */
/* Dada una referencia (puntero a un puntero) al head de la lista y el valor 
a eliminar, elimina la primera ocurrencia del valor en la lista.*/
void deleteNode(struct Node** head_ref, int key)
{
	// Guardamos el nodo head.
	struct Node *temp = *head_ref, *prev;

	// Si el propio nodo head contiene el valor a eliminar.
	if (temp != NULL && temp->data == key) {
		*head_ref = temp->next; // Changed head
		free(temp); // free old head
		return;
	}

	// Buscamos el valor a eliminar, sin perder de vista el nodo anterior ya que
	// tenemos que hay que cambiar 'prev->next'
	while (temp != NULL && temp->data != key) {
		prev = temp;
		temp = temp->next;
	}

	// Si el valor no se encuentra en la lista
	if (temp == NULL)
		return;

	// 'Deslinkeamos' el nodo de la lista
	prev->next = temp->next;

	//Liberamos la memoria del nodo
	free(temp);
	return;
}
```

- **Método recursivo:**
    
    Para eliminar un nodo de manera recursiva hay que seguir los siguientes pasos:
    
    - Pasamos como referencia un puntero a head
    - Puesto que la posición actual del nodo biene dada también por el puntero next del nodo anterior, si cambiamos el valor del puntero del nodo actual, el valor del nodo anterior cambiará también produciendose así la eliminación de un nodo
    
    ```c
    void deleteNode(struct Node** head, int key)
    {
         struct Node* temp;
    		
    		//Comprueba si la lista esta vacía o si hemos llegado al final
        if (*head == NULL) {
            printf("Elemento no presente en la lista\n");
            return;
        }
    		//Si el nodo actual es el que queremos eliminar, si es el primer nodo 
    		//hace que head apunte al segundo, miestras que si es uno intermedio
    		//cambia el valor puntero next del anterior al puntero next actual.
        if ((*head)->data == key) {
            temp = *head;
            *head = (*head)->next; 
    
            free(temp); 
    
            return;
        }
        deleteNode(&(*head)->next, key);
    }
    ```
    
    ### Eliminar un nodo dada su posición
    
    Dada una *linked list* y una posición, eliminar el nodo que se encuentra en dicha posición.
    
    ```c
    void deleteNode(struct Node **head, int pos) 
    { 
       // Si la lista está vacía
       if (*head == NULL) 
          return; 
      
       // Guardamos el nodo head
       struct Node* temp = *head; 
      
        // Si el nodo a eliminar es head 
        if (pos == 0) 
        { 
            *head = temp->next;   // Cambiamos head 
            free(temp);               // Eliminamos el antiguo head 
            return; 
        } 
      
        // Encuentra el nodo anterior al que hay que eliminar
        for (int i = 0; temp != NULL && i < pos - 1; i++) 
             temp = temp->next; 
      
        // Si la posición dada es mayor que el número de nodos de la lista
        if (temp == NULL || temp->next == NULL) 
             return; 
      
        // El nodo temp->next es el nodo que hay que eliminar
        // Guardamos la dirección del nodo siguiente al que tiene que ser eliminado
        struct Node *next = temp->next->next; 
      
        free(temp->next);  // Liberamos memoria  
        temp->next = next;  // 'Deslinkeamos' el nodo eliminado de la lista 
    }
    ```
    

# DOUBLY LINKED LIST

En proceso.

# CIRCULAR LINKED LIST

En proceso.

