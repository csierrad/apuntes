## Sesiones
**tmux** -> crear sesion
**tmux new -s mysession** -> crear una sesion con el nombre mysession

**``tmux kill-ses -t mysession``** -> elimina la sesion con el nombre mysession
**``tmux kill-session -a``** -> elimina todas las sesiones excepto la actual
**``tmux kill-session -a -t mysession``** -> elimina todas las sesiones menos mysession

prefix **$** -> renombrar la sesion
prefix **d** -> detach from session

**`tmux ls`** -> lista todas las sesiones
prefix + **s** -> lista todas las sesiones

**`tmux a`** (attach)-> attach to last session
**`tmux a -t mysession`** -> attach a la sesion con el nombre mysession

prefix **w** -> muestra las sesiones abiertas y las ventanas que 
prefix **(** -> cambiar a la sesion anterior
prefix **)** -> cambiar a la siguiente sesion


## Ventanas
prefix **c** -> crear una nueva ventana
prefix **,** -> renombrar la ventana actual
prefix **&** -> cerrar la ventana actual
prefix **p** -> cambiar a la ventana anterior
prefix **n** -> cambiar a la siguiente ventana
prefix **0..9** -> ir la ventana con el numbero indicado
prefix **l** -> ir a la ultima ventana activa

**: swap-window -s 2 -t 1** -> cambiar de posicion la ventana 2 con la 1
**: swap-window -t -1** -> mueve la ventana actual 1 posicion a la izuierda

> -s  -> source
> -t  -> target


## Paneles
prefix **"** -> divide el panel horizontalmente
prefix **%** -> divide el panel verticalmente
prefix **;** -> cambia al ultimo panel activo
prefix **{** -> mueve el panel actual a la izquierda
prefix **}** -> mueve el panel actual a la derecha
prefix **arrows** -> cambiar al panel en la direccion indicada
prefix + **arrows** -> cambiar el tamaño del panel actual 

prefix **Space** -> cambia entre distintos layouts de paneles predefinidos 
prefix **o** -> cambia al siguiente panel
prefix + **o** -> intercambia todos los paneles en sentido horario
prefix **q** -> muestra el numero de los paneles
prefix **q + 0..9** -> cambia al panel indicado
prefix **z** -> alterna entre pantalla completa
prefix **!** -> convierte un panel en una ventana
prefix **x** -> cierra el panel actual

## Copy mode
prefix **\[** ->  entrar en copy mode
prefix **pgup** -> entrar en copy mode y avanzar una pagina
**q** -> salir del copy mode

**arrows** -> mover el cursor
**h j k l** -> mover el cursor 
**w** -> mover el cursor una palabra hacia delante
**b** -> mover el cursor una palabra hacia atras
**/** -> buscar hacia delante
**?** -> buscar hacia atras
**n** -> siguinte palabraencontrada
**N** -> anterior palabra encontrada
**Space** -> empezar la seleccion
**Esc** -> limpiar la seleccion
**Enter** -> copiar la seleccion
**prefix ]** -> pegar el contenido del buffer_0

**: show-buffer** -> muestra el contenido del buffer_0
**: capture-pane** -> copia todo el contenido visible del panel en un buffer
**: list-buffers** -> muestra todos los buffers
**: choose-buffer** -> muestra todos los buffers y pega el seleccionado
**: save-buffer buf.txt** -> guarda el contenido del buffer en buf.txt
**: delete-buffer -b 1** -> elimina el buffer_1


## Misc
prefix **:** -> entrar en modo comandos