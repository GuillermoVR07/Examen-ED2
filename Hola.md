# Explicación Técnica del Visualizador de Árbol Binario

Este documento detalla el funcionamiento interno de la aplicación, desde la estructura de datos hasta la graficación y las lógicas de espejo.

## 1. Creación y Almacenamiento de Nodos y Aristas

La base del proyecto son dos clases de Python que definen la estructura del árbol.

### ¿Cómo se crean los Nodos y las Aristas?

- **Nodos**: Se utiliza una clase llamada `Nodo`. Cada vez que insertas un número, se crea un objeto (una instancia) de esta clase. Cada objeto `Nodo` tiene tres atributos principales:
  1.  `valor`: Guarda el número que insertaste (por ejemplo, 50, 25, 75). Este es el dato del nodo.
  2.  `hijo_izquierdo`: Un puntero que puede apuntar a otro objeto `Nodo`. Inicialmente es `None` (vacío).
  3.  `hijo_derecho`: Igual que el anterior, pero para el lado derecho. También es `None` al principio.

- **Aristas (Conexiones)**: Las aristas no son objetos separados. Son las **relaciones** o **punteros** entre los nodos. Cuando insertas un número menor que un nodo padre (por ejemplo, insertas 20 cuando el padre es 50), el atributo `hijo_izquierdo` del nodo 50 deja de ser `None` y pasa a apuntar al nuevo objeto `Nodo` que contiene el 20. Esa conexión es la arista.

### ¿Dónde y cómo se guardan estos datos?

- **Tipo de Dato**: Los datos se guardan como objetos de las clases `Nodo` y `ArbolBinario`.
- **Lugar de Almacenamiento**: Toda la estructura del árbol se guarda en una **variable global** en el archivo `app.py`, llamada `arbol`. Esta variable es una instancia de la clase `ArbolBinario`, que solo necesita guardar una referencia al nodo `raiz`.
- **Importante**: Como es una variable en memoria, **el árbol se borra y se reinicia cada vez que el servidor de Flask se detiene y se vuelve a iniciar**.

## 2. Graficación del Árbol

La visualización del árbol no usa librerías de grafos, sino que se dibuja directamente con **Matplotlib**.

El proceso se divide en dos funciones clave:

### `obtener_posiciones(raiz)`

Esta es la función más importante para la apariencia del árbol. Su objetivo es asignar una coordenada `(x, y)` a cada nodo para que no se superpongan.

- **Coordenada Y**: Se determina por el nivel o la profundidad del nodo en el árbol. El nodo raíz está en el nivel 0, sus hijos en el -1, sus nietos en el -2, y así sucesivamente.
- **Coordenada X**: Para evitar que el árbol se vea desorganizado, la coordenada `x` se calcula realizando un **recorrido in-order** del árbol. Se usa un contador global (`next_x`) que aumenta cada vez que se visita un nodo. Esto garantiza que los nodos de la izquierda siempre tengan una coordenada `x` menor que sus padres, y los de la derecha una mayor, creando el espaciado horizontal característico de un árbol.

### `dibujar_arbol(raiz)`

Una vez que cada nodo tiene sus coordenadas, esta función se encarga de "pintar":

1.  **Dibuja las Aristas**: Recorre las conexiones padre-hijo y usa `ax.plot()` de Matplotlib para trazar una línea recta entre las coordenadas del padre y las del hijo.
2.  **Dibuja los Nodos**: Itera sobre las posiciones calculadas y, para cada coordenada, dibuja un círculo (`plt.Circle`) y escribe el valor del nodo dentro del círculo (`ax.text`).
3.  **Guarda la Imagen**: Finalmente, guarda todo el dibujo como un archivo de imagen (`static/tree.png`), que es el que se muestra en la página web.

## 3. Funciones de Espejo

### Contar Filas Espejo

- **Objetivo**: Contar cuántos **niveles** o **filas** del árbol son estructuralmente simétricos.
- **Función Principal**: `contar_filas_espejo()`.
- **¿Cómo funciona?**: Itera nivel por nivel (fila por fila) desde la parte alta del árbol hacia abajo. En cada nivel, llama a una función auxiliar `son_nodos_en_el_nivel_reflejado()` para comprobar si esa fila específica es un espejo.
- **Lógica Clave (`son_nodos_en_el_nivel_reflejado`)**: Es una función recursiva que baja hasta el nivel que se le pide. Una vez allí, comprueba la simetría: que el hijo izquierdo de una rama se corresponda con el hijo derecho de la otra, y viceversa. Si en algún nivel la simetría se rompe, el conteo se detiene.

### Contar Nodos en Columnas Espejo

- **Objetivo**: Contar cuántos **nodos individuales** forman parte de la estructura de espejo, no solo las filas.
- **Función Principal**: `contar_nodos_espejo()`.
- **¿Cómo funciona?**: Llama a una función recursiva auxiliar `_contar_nodos_espejo_recursivo()` que viaja por las dos ramas principales del árbol (izquierda y derecha de la raíz).
- **Lógica Clave (`_contar_nodos_espejo_recursivo`)**: Compara dos nodos en posiciones simétricas. Si ambos existen, suma `2` al contador y luego se llama a sí misma para los hijos en posiciones de espejo (el hijo izquierdo de uno con el derecho del otro). Si en algún punto una de las ramas tiene un nodo y la otra no, esa ruta de exploración se detiene y no se suman más nodos, ya que la simetría se rompió.
