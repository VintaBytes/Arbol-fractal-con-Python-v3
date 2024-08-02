# Arbol fractal con Python v3

Otro script que utiliza la librería `turtle` en Python para dibujar un árbol fractal. El árbol se genera utilizando parámetros predefinidos y funciones recursivas para crear un dibujo detallado y aleatorio.
Se han agregado "hojas", y un coloreado aleatorio para conseguir un mejor resultado.

<span><img src="https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue"/></span>
<span><img src="https://img.shields.io/badge/VSCode-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white"/></span>

## Resultado
<img src="https://github.com/VintaBytes/Arbol-fractal-con-Python-v2/blob/main/lsystem-21.jpeg?raw=true" width="640px">

## Explicación del Código

### Importaciones
```python
import turtle
import random
import time
```
El código importa las librerías `turtle` para el dibujo, `random` para generar variaciones aleatorias y `time` para manejar pausas.

### Variables Globales
```python
ANG = 20
RAND = 20
REL = 4/5
RANDT = 100
GROSORTRONCO = 0
TAMINIC = 100
TAMHOJA = 10
ANGHOJA = 90
PROF = 12

CTRONCO = (165, 42, 42)
CTRONCOVAR = 15
CHOJAS = (100, 200, 30)
CHOJASVAR = 40
CFONDO = (255, 255, 255)
```
- `ANG`, `RAND`, `REL`, `RANDT`: Parámetros de control del ángulo y tamaño de las ramas y sub-ramas.
- `GROSORTRONCO`, `TAMINIC`, `TAMHOJA`, `ANGHOJA`, `PROF`: Parámetros del grosor del tronco, tamaño inicial y tamaño y ángulo de las hojas.
- `CTRONCO`, `CTRONCOVAR`, `CHOJAS`, `CHOJASVAR`, `CFONDO`: Parámetros de color del tronco, hojas y fondo, junto con su variación.

### Función `arbol`
```python
def arbol(t, d):
    if d == 0:
        turtle.forward(t)
        hoja(TAMHOJA, ANGHOJA)
        turtle.penup()
        turtle.back(t)
        turtle.pendown()
        turtle.color(CTRONCO)
        return
    else:
        angulo1 = ANG + random.randrange(-RAND, RAND + 1)
        angulo2 = ANG + random.randrange(-RAND, RAND + 1)
        tamano = t + t * random.randrange(-RANDT, RANDT + 1) / 100
        colortronco = variacioncolor(CTRONCO, CTRONCOVAR)
        turtle.color(colortronco)
        turtle.pensize(d + GROSORTRONCO)
        turtle.forward(tamano)
        turtle.left(angulo1)
        arbol(t * REL, d - 1)
        turtle.right(angulo1 + angulo2)
        arbol(t * REL, d - 1)
        turtle.color(colortronco)
        turtle.left(angulo2)
        turtle.penup()
        turtle.back(tamano)
        turtle.pendown()
```
Esta función es recursiva y dibuja el árbol fractal. Los parámetros son:
- `t`: Tamaño del segmento.
- `d`: Profundidad de recursión.
La función ajusta el ángulo y tamaño de las ramas aleatoriamente y llama a sí misma para dibujar las sub-ramas.

### Función `hoja`
```python
def hoja(t, a):
    turtle.color(variacioncolor(CHOJAS, CHOJASVAR))
    turtle.begin_fill()
    turtle.right(a / 2)
    turtle.circle(t, a)
    turtle.left(180 - a)
    turtle.circle(t, a)
    turtle.left(180 - a / 2)
    turtle.end_fill()
```
Dibuja una hoja en la posición actual del turtle. Los parámetros son:
- `t`: Tamaño de la hoja.
- `a`: Ángulo de las puntas de las hojas.

### Función `variacioncolor`
```python
def variacioncolor(color, var):
    Rd = random.randrange(-var, var + 1)
    Gd = random.randrange(-var, var + 1)
    Bd = random.randrange(-var, var + 1)
    R, G, B = color
    R += Rd
    G += Gd
    B += Bd
    R = max(0, min(255, R))
    G = max(0, min(255, G))
    B = max(0, min(255, B))
    return R, G, B
```
Genera una variación de color RGB. Los parámetros son:
- `color`: Color base.
- `var`: Cantidad de variación permitida.

### Función `init`
```python
def init():
    turtle.speed(0)
    turtle.colormode(255)
    turtle.clear()
    turtle.penup()
    turtle.home()
    turtle.left(90)
    turtle.back(200)
    turtle.pendown()
    turtle.hideturtle()
    turtle.color(CTRONCO)
    turtle.bgcolor(CFONDO)
    arbol(TAMINIC, PROF)
    turtle.done()
```
Inicializa la posición del turtle y llama a la función `arbol` para comenzar el dibujo.

### Configuración y Ejecución
```python
turtle.setup(1024, 800, 0, 0)
turtle.penup()
turtle.goto(0, -450)
turtle.pendown()
time.sleep(8)
init()
turtle.exitonclick()
```
- `turtle.setup(...)`: Configura el tamaño de la ventana.
- `turtle.penup()`, `turtle.goto(...)`, `turtle.pendown()`: Posiciona el turtle.
- `time.sleep(8)`: Pausa antes de comenzar.
- `init()`: Llama a la función de inicialización.
- `turtle.exitonclick()`: Espera un clic para cerrar la ventana.
