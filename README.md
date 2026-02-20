#  Práctica: Creación de un Polígono 2D en Blender mediante Python

##  Objetivo

Crear un polígono regular en 2D dentro de Blender **sin modelarlo manualmente**, usando un script en Python que calcule automáticamente la posición de sus vértices.


#  PASO A PASO


##  Paso 1: Abrir Blender

1. Abre **Blender**
2. Aparecerá la escena inicial con:

   * Un cubo
   * Una cámara
   * Una luz

---

##  Paso 2: Cambiar al espacio de trabajo de Scripting

En la parte superior de Blender verás varias pestañas como:

* Layout
* Modeling
* Sculpting
* UV Editing
* Texture Paint
* Shading
* Animation

Debes hacer clic en:

 **Scripting**

![Image](https://static.wixstatic.com/media/ec68c9_30634babab0746078f94bc0d98550e1d~mv2.jpeg/v1/fill/w_980%2Ch_551%2Cal_c%2Cq_85%2Cusm_0.66_1.00_0.01%2Cenc_avif%2Cquality_auto/ec68c9_30634babab0746078f94bc0d98550e1d~mv2.jpeg)

![Image](https://docs.blender.org/manual/en/3.3/_images/interface_window-system_workspaces_layout.png)

![Image](https://tabreturn.github.io/img/aqitbcc01/getting-started-blender.png)

![Image](https://docs.blender.org/manual/en/latest/_images/render_freestyle_python_scripting-mode.png)

Esto abrirá:

 Editor de texto (para escribir código)
 Consola de Python
 Vista 3D


##  Paso 3: Crear un nuevo script

1. En el editor de texto haz clic en:

 **New**

Esto creará un archivo vacío donde escribirás el código.

![Image](https://i.sstatic.net/1XeYL.png)

![Image](https://blender-addons.org/app/uploads/2024/07/character_count.jpg)

![Image](https://static.wixstatic.com/media/ec68c9_53481a5c271048738651368dd34df9a8~mv2.jpeg/v1/fill/w_1000%2Ch_563%2Cal_c%2Cq_85%2Cusm_0.66_1.00_0.01/ec68c9_53481a5c271048738651368dd34df9a8~mv2.jpeg)

![Image](https://i.sstatic.net/DwNHL.jpg)

##  Paso 4: Entender qué vamos a hacer

El script hará 4 cosas automáticamente:

1. Borrar el cubo inicial
2. Calcular los vértices del polígono
3. Crear la malla
4. Dibujar el polígono en la escena

---

##  Paso 5: Copiar el código

Copia y pega esto en el editor:

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
```

---

##  Paso 6: ¿Qué hace cada parte?

###  Importaciones

```python
import bpy
import math
```

* `bpy` → permite controlar Blender con Python
* `math` → permite usar seno y coseno

---

###  Crear la malla

```python
malla = bpy.data.meshes.new(nombre)
objeto = bpy.data.objects.new(nombre, malla)
bpy.context.collection.objects.link(objeto)
```

Esto:

Crea la figura
La agrega a la escena


###  Calcular vértices

```python
for i in range(lados):
    angulo = 2 * math.pi * i / lados
    x = radio * math.cos(angulo)
    y = radio * math.sin(angulo)
    vertices.append((x, y, 0))
```

Aquí se usa:

Trigonometría

Cada punto se coloca en una circunferencia imaginaria.



### 📌 Conectar vértices

```python
for i in range(lados):
    aristas.append((i, (i+1)%lados))
```

Esto une:

Vértice 0 → 1
1 → 2
2 → 3
...
Último → Primero

Así se cierra la figura.

---

###  Crear el polígono

```python
malla.from_pydata(vertices, aristas, [])
malla.update()
```

Construye la figura en Blender.



###  Borrar el cubo inicial

```python
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```

Limpia la escena antes de crear el polígono.



###  Crear el polígono

```python
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```

Esto genera:

Un hexágono


##  Paso 7: Ejecutar el script

Haz clic en:

 **Run Script**

![Image](https://blenderartists.org/uploads/default/original/3X/b/6/b63fae4635cb3fa8900788450a4ea64f252040a2.png)

![Image](https://i.stack.imgur.com/zAzFw.gif)



##  Paso 8: Resultado

Verás aparecer en la escena:

✔ Un polígono 2D
✔ De 6 lados
✔ Con radio 5

Sin haber modelado nada manualmente 😎



#  Puedes modificar

Cambiar lados:

```python
lados=8
```

Cambiar tamaño:

```python
radio=3
```

Ejemplo:

```python
crear_poligono_2d("Poligono2D", lados=10, radio=2)
```

→ Creará un decágono.



# Conclusión

Con este proceso aprendiste a:

✔ Automatizar modelado
✔ Aplicar matemáticas en gráficos
✔ Crear geometría con código
✔ Usar scripting en Blender

---

Si quieres, puedo ayudarte a que ahora el polígono tenga **relleno (cara)** o que se convierta en **3D** 🚀
