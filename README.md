# Visualizador de Árbol Binario

Una aplicación web simple creada con Flask que permite visualizar un Árbol Binario de Búsqueda, insertar nodos y ejecutar funciones especiales sobre la estructura del árbol.

## Funcionalidades

- **Inserción de Nodos**: Añade nodos al árbol. La aplicación actualizará la visualización automáticamente.
- **Visualización Gráfica**: Muestra una representación gráfica del árbol que se actualiza con cada inserción.
- **Borrado Total**: Un botón para eliminar el árbol completo y empezar desde cero.
- **Contar Filas Espejo**: Calcula el número de niveles (filas) que son estructuralmente un espejo el uno del otro, hasta una altura máxima especificada.
- **Contar Nodos Espejo**: Cuenta el número total de nodos que forman parte de una estructura de "columnas" en espejo, hasta una altura máxima especificada.

## Instalación y Puesta en Marcha

Sigue estos pasos para configurar y ejecutar el proyecto en tu máquina local.

### 1. Clonar el Repositorio (Si aplica)

Si estás trabajando desde un repositorio Git, primero clónalo:
```bash
git clone <url-del-repositorio>
cd <nombre-del-directorio>
```

### 2. Crear y Activar un Entorno Virtual

Es una buena práctica usar un entorno virtual para aislar las dependencias del proyecto. Desde la raíz del directorio del proyecto, ejecuta:

```bash
# Crear el entorno virtual (puedes nombrarlo 'venv' o como prefieras)
python -m venv venv

# Activar el entorno en Windows
.\venv\Scripts\activate
```

### 3. Instalar las Dependencias

Una vez que el entorno virtual esté activado, instala todas las librerías necesarias usando el archivo `requirements.txt`.

```bash
pip install -r requirements.txt
```

### 4. Ejecutar la Aplicación

Con las dependencias instaladas, puedes iniciar el servidor de Flask:

```bash
python app.py
```

### 5. Acceder a la Aplicación

Una vez que el servidor esté en marcha, abre tu navegador web y ve a la siguiente dirección:

[http://127.0.0.1:5000](http://127.0.0.1:5000)

¡Y eso es todo! Ahora puedes interactuar con el visualizador de árbol binario.
