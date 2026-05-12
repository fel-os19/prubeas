# Mapa Turístico y Rutas con Teoría de Grafos

Proyecto semestral desarrollado en lenguaje C para la asignatura **Matemáticas Discretas** de la carrera **Ingeniería Civil Informática** de la Universidad de Concepción.

El programa modela un mapa turístico a partir de calles definidas por coordenadas y puntos de interés ubicados sobre ellas. Luego transforma esa información en un **grafo ponderado no dirigido** y utiliza el algoritmo de **Dijkstra** para calcular rutas entre los puntos turísticos.

---

## Tabla de contenidos

- [Descripción general](#descripción-general)
- [Modelo del problema](#modelo-del-problema)
- [Funcionamiento del programa](#funcionamiento-del-programa)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Requisitos](#requisitos)
- [Compilación](#compilación)
- [Ejecución](#ejecución)
- [Formato del archivo de entrada](#formato-del-archivo-de-entrada)
- [Ejemplo de entrada](#ejemplo-de-entrada)
- [Ejemplo de funcionamiento](#ejemplo-de-funcionamiento)
- [Versión gráfica experimental](#versión-gráfica-experimental)
- [Limitaciones](#limitaciones)
- [Posibles mejoras](#posibles-mejoras)
- [Autores](#autores)

---

## Descripción general

Este proyecto permite representar el mapa turístico de una ciudad mediante teoría de grafos. Para ello, el programa recibe como entrada un archivo de texto que contiene:

- Calles definidas por coordenadas iniciales y finales.
- Un eje de numeración para cada calle.
- Puntos turísticos ubicados sobre calles existentes.

A partir de esos datos, el programa construye un grafo donde:

- Los **vértices** representan extremos de calles, intersecciones y puntos turísticos.
- Las **aristas** representan tramos transitables entre vértices consecutivos.
- Los **pesos** representan la distancia geométrica entre dos vértices conectados.

Una vez construido el grafo, el programa calcula rutas entre puntos turísticos utilizando el algoritmo de **Dijkstra**, mostrando por consola las instrucciones necesarias para recorrer el mapa.

---

## Modelo del problema

El programa transforma un problema geométrico en un problema de grafos.

El proceso general es el siguiente:

```text
Archivo de entrada
        ↓
Lectura de calles y puntos turísticos
        ↓
Representación de calles como segmentos en el plano cartesiano
        ↓
Detección de extremos, intersecciones y puntos turísticos
        ↓
Creación de vértices del grafo
        ↓
Conexión de vértices consecutivos mediante aristas
        ↓
Asignación de pesos según distancia
        ↓
Aplicación de Dijkstra para calcular rutas
```

El programa no construye el grafo a partir de una figura cerrada o de un cuadrado. En cambio, interpreta cada calle como una línea definida por coordenadas. Los extremos de esas líneas se transforman en vértices, y cuando dos calles se cruzan, la intersección también se incorpora como un vértice compartido.

---

## Funcionamiento del programa

El programa principal se encuentra en el archivo `mapa.c`.

Su funcionamiento se puede resumir en las siguientes etapas:

### 1. Lectura del archivo

El programa solicita al usuario el nombre de un archivo de texto. Este archivo debe contener la información de calles y puntos turísticos.

### 2. Construcción del mapa geométrico

Cada calle se interpreta como un segmento dentro de un plano cartesiano, usando sus coordenadas iniciales y finales.

### 3. Creación de vértices

Se crean vértices en:

- Los extremos de cada calle.
- Las intersecciones entre calles.
- Los puntos turísticos definidos en el archivo.

### 4. Construcción del grafo

Los vértices ubicados sobre una misma calle se ordenan según su posición dentro del segmento. Luego se conectan solo los vértices consecutivos.

Por ejemplo, si sobre una calle existen estos puntos:

```text
(0,50), (300,50), (650,50), (900,50), (1200,50)
```

El programa crea las siguientes conexiones:

```text
(0,50)    ↔ (300,50)
(300,50)  ↔ (650,50)
(650,50)  ↔ (900,50)
(900,50)  ↔ (1200,50)
```

De esta manera, el grafo mantiene la forma real del mapa y evita crear conexiones que no existen en las calles originales.

### 5. Cálculo de rutas

Para calcular caminos entre puntos turísticos, el programa utiliza el algoritmo de **Dijkstra**. Cada arista tiene un peso correspondiente a la distancia entre dos vértices, por lo que Dijkstra permite encontrar el camino de menor distancia entre un punto turístico de origen y otro de destino.

### 6. Marcado automático de puntos visitados

Si durante una ruta el programa pasa por un punto turístico que aún no había sido visitado, este se marca automáticamente como visitado. Esto permite evitar recorridos innecesarios cuando un punto turístico ya fue alcanzado durante el trayecto.

---

## Estructura del proyecto

La entrega contiene los siguientes archivos principales:

```text
Tarea_Grafos_Grupo_Fernandez_Dominguez_Grandon/
│
├── mapa.c
├── input.txt
├── input2.txt
├── input3.txt
├── InformeDiscreta.pdf
├── README.md
│
└── version_grafica/
    ├── versiongrafica.c
    ├── versiongrafica2.c
    └── README2.md
```

### Descripción de archivos

| Archivo | Descripción |
|---|---|
| `mapa.c` | Código fuente principal del programa oficial por consola. |
| `input.txt` | Archivo de entrada de prueba. |
| `input2.txt` | Segundo archivo de entrada de prueba. |
| `input3.txt` | Tercer archivo de entrada de prueba. |
| `InformeDiscreta.pdf` | Informe del proyecto. |
| `README.md` | Documentación principal del proyecto. |
| `version_grafica/` | Carpeta con una versión gráfica experimental. |

---

## Requisitos

Para compilar y ejecutar la versión oficial del programa se requiere:

- Sistema operativo Linux o entorno compatible.
- Compilador `gcc`.
- Librería matemática estándar de C (`math.h`).

El programa utiliza funciones matemáticas como `sqrt`, `fabs`, `fmin` y `fmax`, por lo que es necesario enlazar la librería matemática con la bandera `-lm`.

---

## Compilación

Ubicarse en la carpeta donde se encuentra el archivo `mapa.c` y ejecutar:

```bash
gcc mapa.c -o mapa -lm
```

También se puede compilar mostrando advertencias del compilador:

```bash
gcc -Wall -Wextra -std=c11 mapa.c -o mapa -lm
```

---

## Ejecución

Una vez compilado, ejecutar el programa con:

```bash
./mapa
```

El programa solicitará el nombre del archivo de entrada:

```text
Ingrese el nombre del archivo de texto a leer:
```

Por ejemplo:

```text
input3.txt
```

Si el archivo es válido, el programa leerá las calles, construirá el grafo y mostrará por consola la ruta calculada.

---

## Formato del archivo de entrada

El archivo de entrada debe tener la siguiente estructura:

```text
N
Nombre_calle x1 y1 x2 y2 Eje
Nombre_calle x1 y1 x2 y2 Eje
...
M
Nombre_punto Nombre_calle posicion
Nombre_punto Nombre_calle posicion
...
```

Donde:

| Elemento | Descripción |
|---|---|
| `N` | Cantidad de calles. |
| `Nombre_calle` | Nombre de la calle. No debe contener espacios. |
| `x1 y1` | Coordenadas iniciales de la calle. |
| `x2 y2` | Coordenadas finales de la calle. |
| `Eje` | Puede ser `X` o `Y`. Indica cómo se interpreta la posición de los puntos turísticos. |
| `M` | Cantidad de puntos turísticos. |
| `Nombre_punto` | Nombre del punto turístico. No debe contener espacios. |
| `Nombre_calle` | Calle donde se ubica el punto turístico. |
| `posicion` | Posición del punto turístico sobre la calle, según el eje de numeración. |

---

## Ejemplo de entrada

```text
4
Los_Carrera 0 50 1200 50 X
Freire 0 200 1200 200 X
Janequeo 650 0 650 800 Y
Tucapel 900 0 900 800 Y
2
Museo Los_Carrera 300
Plaza Freire 900
```

En este ejemplo:

- `Los_Carrera` es una calle horizontal desde `(0,50)` hasta `(1200,50)`.
- `Freire` es una calle horizontal desde `(0,200)` hasta `(1200,200)`.
- `Janequeo` es una calle vertical desde `(650,0)` hasta `(650,800)`.
- `Tucapel` es una calle vertical desde `(900,0)` hasta `(900,800)`.
- `Museo` se ubica sobre `Los_Carrera` en la posición `300`, equivalente a la coordenada `(300,50)`.
- `Plaza` se ubica sobre `Freire` en la posición `900`, equivalente a la coordenada `(900,200)`.

---

## Ejemplo de funcionamiento

Una ejecución del programa puede verse de la siguiente manera:

```text
Ingrese el nombre del archivo de texto a leer: input3.txt

Archivo cargado correctamente.

Punto de partida: Museo

Viajando hacia: Plaza

Avanza por Los_Carrera.
Avanza por Janequeo.
Avanza por Freire.

Punto turístico alcanzado: Plaza

Todos los puntos turísticos fueron visitados.
```

La salida exacta puede variar dependiendo del archivo de entrada y de los puntos turísticos definidos.

---

## Principales funciones del programa

| Función | Descripción |
|---|---|
| `leer_archivo()` | Lee las calles y puntos turísticos desde el archivo de entrada. |
| `agregar_nodo()` | Agrega un nodo al grafo evitando duplicar coordenadas ya existentes. |
| `interseccion_segmentos()` | Determina si dos calles se intersectan y calcula el punto de cruce. |
| `construir_grafo()` | Genera los vértices, detecta intersecciones, ordena puntos sobre cada calle y crea las aristas. |
| `dijkstra()` | Calcula el camino de menor distancia entre dos nodos del grafo. |
| `calcular_y_mostrar_ruta()` | Controla el recorrido completo entre puntos turísticos y muestra las instrucciones por consola. |
| `liberar_grafo()` / `limpiar_adyacencia()` | Libera la memoria dinámica utilizada por las listas de adyacencia. |

---

## Versión gráfica experimental

Además de la versión principal por consola, se incluye una versión gráfica experimental.

Esta versión fue utilizada para explorar visualmente el modelo del mapa y probar una estrategia adicional de optimización del recorrido. No corresponde a la versión oficial principal, ya que puede depender de librerías específicas del entorno Windows.

Para compilar la versión gráfica en Windows con MinGW, usar el comando correspondiente al archivo que se desea probar.

Por ejemplo:

```cmd
gcc versiongrafica.c -o versiongrafica.exe -lgdi32 -luser32 -lm
```

o, para la segunda versión:

```cmd
gcc versiongrafica2.c -o versiongrafica2.exe -lgdi32 -luser32 -lm
```

La versión gráfica puede incluir funciones adicionales fuera del alcance de la entrega principal, como visualización del mapa o exploración de recorridos alternativos.

---

## Limitaciones

La versión principal del programa calcula rutas entre puntos turísticos siguiendo un criterio secuencial. Esto significa que parte desde el primer punto turístico indicado en el archivo y avanza hacia los siguientes puntos no visitados.

Por esta razón, el programa no necesariamente encuentra el recorrido global más corto que visite todos los puntos turísticos. Su objetivo principal es construir correctamente el grafo ponderado y aplicar Dijkstra para obtener caminos de menor distancia entre puntos turísticos.

Otras consideraciones:

- Los nombres de calles y puntos turísticos no deben contener espacios.
- El eje de numeración debe ser `X` o `Y`.
- Cada punto turístico debe estar asociado a una calle existente.
- Las distancias se calculan usando geometría euclidiana.
- La versión principal está orientada a ejecución por consola.
- La versión gráfica es experimental y no reemplaza la versión oficial.

---

## Posibles mejoras

Algunas mejoras futuras para el proyecto son:

- Incorporar una validación más detallada de puntos turísticos fuera del rango de una calle.
- Exportar la ruta final a un archivo de texto.
- Incorporar una visualización gráfica multiplataforma.
- Mostrar estadísticas más detalladas del recorrido.
- Optimizar globalmente el orden de visita de los puntos turísticos.
- Implementar una interfaz más interactiva para seleccionar origen y destino.
- Agregar soporte para nombres de calles con espacios.

---

## Autores

- Rodrigo Domínguez Larenas
- Ariel Fernández Fuentealba
- Felipe Grandón Contreras

---

## Profesora

- Lilian Angélica Salinas Ayala

---

## Asignatura

**Matemáticas Discretas**  
**Ingeniería Civil Informática**  
**Universidad de Concepción**

---

## Uso académico

Este proyecto fue desarrollado con fines académicos para aplicar contenidos de teoría de grafos, estructuras de datos y algoritmos de búsqueda de caminos en un problema de modelamiento computacional.
