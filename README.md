<h1 align="center">Practica: Creacion de un Poligono 2D en Blender mediante Python</h1>

<p align="center">
Uso de scripting en Blender para la generacion automatica de figuras geometricas
</p>

---

## Introduccion

Blender permite automatizar la creacion de objetos mediante el uso de Python.  
En esta practica se desarrolla un script que genera un poligono regular en 2D utilizando calculos matematicos basados en coordenadas polares.

El objetivo es comprender como:

- Crear objetos mediante codigo
- Generar vertices de forma automatica
- Aplicar trigonometria en graficos
- Construir figuras geometricas sin modelado manual

---

## Descripcion del problema

Se requiere crear un poligono regular sin usar herramientas de modelado manual, utilizando un algoritmo que:

1. Calcule la posicion de cada vertice
2. Genere la malla del objeto
3. Conecte los vertices mediante aristas
4. Dibuje el poligono dentro de la escena

---

## Fundamento teorico

Un poligono regular puede generarse distribuyendo sus vertices sobre una circunferencia.

Cada vertice se obtiene con:

x = r * cos(angulo)  
y = r * sin(angulo)

Donde:

- r es el radio
- angulo = (2π * i) / n
- n es el numero de lados
- i es la posicion del vertice

Esto permite ubicar puntos equidistantes formando la figura.

---

## Requisitos

- Blender 5.0 o superior
- Editor de scripting activado

---

## Procedimiento

### Paso 1: Abrir Blender

Seleccionar el espacio de trabajo:

Scripting

---

### Paso 2: Crear un nuevo script

<img width="750" height="716" alt="script" src="https://github.com/user-attachments/assets/b38fbb78-59d8-44c6-b0f1-7a80f401337a" />

---

### Paso 3: Insertar el siguiente codigo

```python
import bpy
import math

def crear_poligono_2d(nombre, lados, radio):

    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)
    bpy.context.collection.objects.link(objeto)

    vertices = []
    aristas = []

    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0))

    for i in range(lados):
        aristas.append((i, (i+1)%lados))

    malla.from_pydata(vertices, aristas, [])
    malla.update()

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

crear_poligono_2d("Poligono2D", lados=6, radio=5)
#Resultados:
<img width="408" height="242" alt="resultado" src="https://github.com/user-attachments/assets/c40ac146-8b75-4ed5-bee6-0e042c7f0f9b" />
