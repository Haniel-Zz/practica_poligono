# 🧩 Práctica: Dibujo de un Polígono en Blender con Python

## 📌 Descripción

Esta práctica muestra cómo crear un polígono de *n lados* utilizando Python dentro de Blender.

El script permite:

- Crear una malla nueva  
- Generar vértices usando coordenadas polares  
- Conectar los vértices para formar el polígono  
- Dibujar automáticamente la figura en 2D  

---

## ⚙️ Requisitos

- Blender 5.0 o superior
- Editor de scripting activado

---

## ▶️ Pasos para realizar la práctica

### 1. Abrir Blender

Ir a:

Scripting

---

### 2. Crear un nuevo Script

---

### 3. Copiar el siguiente código

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
