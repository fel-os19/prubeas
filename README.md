# Mapa Turístico con Teoría de Grafos

Proyecto desarrollado en lenguaje C para la asignatura **Matemáticas Discretas** de la carrera **Ingeniería Civil Informática** de la Universidad de Concepción.

El programa permite modelar un mapa turístico a partir de calles definidas por coordenadas y puntos de interés ubicados sobre ellas. Con esta información, construye un grafo ponderado y utiliza el algoritmo de Dijkstra para calcular rutas entre los puntos turísticos.

## Integrantes

- Rodrigo Domínguez Larenas
- Ariel Fernández Fuentealba
- Felipe Grandón Contreras

## Archivos principales

```text
mapa.c
input.txt
input2.txt
input3.txt
InformeDiscreta.pdf
README.md
```

Además, se incluye una carpeta con una versión gráfica experimental desarrollada como complemento del proyecto.

## Requisitos

Para compilar la versión oficial se requiere:

- Sistema operativo Linux o entorno compatible.
- Compilador `gcc`.
- Librería matemática estándar de C.

## Compilación

Desde la carpeta donde se encuentra `mapa.c`, ejecutar:

```bash
gcc mapa.c -o mapa -lm
```

También puede compilarse mostrando advertencias:

```bash
gcc -Wall -Wextra -std=c11 mapa.c -o mapa -lm
```

## Ejecución

Después de compilar, ejecutar:

```bash
./mapa
```

El programa solicitará el nombre del archivo de entrada. Por ejemplo:

```text
input.txt
```

También pueden usarse los otros archivos de prueba incluidos:

```text
input2.txt
input3.txt
```

## Formato general del archivo de entrada

El archivo debe indicar primero las calles y luego los puntos turísticos:

```text
N
Nombre_calle x1 y1 x2 y2 Eje
...
M
Nombre_punto Nombre_calle posicion
...
```

Donde `N` corresponde a la cantidad de calles y `M` a la cantidad de puntos turísticos.  
El eje puede ser `X` o `Y`, según cómo se ubica el punto turístico sobre la calle.

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

## Versión gráfica experimental

La versión oficial del proyecto es `mapa.c`, ejecutada por consola.

También se incluye una versión gráfica experimental como complemento. Esta versión utiliza dependencias de Windows, por lo que no está pensada para compilarse directamente en Linux.

Para compilarla en Windows con MinGW:

```cmd
gcc versiongrafica.c -o versiongrafica.exe -lgdi32 -luser32 -lm
```

o:

```cmd
gcc versiongrafica2.c -o versiongrafica2.exe -lgdi32 -luser32 -lm
```

## Consideraciones

- Los nombres de calles y puntos turísticos no deben contener espacios.
- Cada punto turístico debe estar asociado a una calle existente.
- La versión oficial calcula rutas mediante Dijkstra.
- El informe contiene la explicación completa del modelo, la implementación y las conclusiones.

## Profesora

Lilian Angélica Salinas Ayala
