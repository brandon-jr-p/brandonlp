# PRIMER REPOSITORIO

## 1. Instalacion de Blender


### Paso 1

Primero tenemos que ir al navegador y colocar Blender y buscamos el apartado donde diga Download-Blender y le damos clic para abrir 

<img width="1920" height="1080" alt="Captura de pantalla (64)" src="https://github.com/user-attachments/assets/dca0723a-e53e-4c56-b6ed-36d66954f7cc" />


### Paso 2

Una vez ya que le dimos abrir nos aparecera lo siguiente:

<img width="1920" height="1080" alt="Captura de pantalla (65)" src="https://github.com/user-attachments/assets/8a9fda9b-f359-4415-a63f-312748e0dcfc" />


### Paso 3

Le daremos instalar, una vez ya instalado le daremos click para abrirlo en nuestra carpeta

<img width="1920" height="1080" alt="Captura de pantalla (66)" src="https://github.com/user-attachments/assets/307f4cf2-5427-47e5-b4c8-ff30cc50dac0" />


### Paso 4

Una vez abierta nuestra carpeta buscaremos el apartado donde dice "descargas" le daremos click en la carpeta y buscaremos nuestro instalador y le daremos click

<img width="1920" height="1080" alt="Captura de pantalla (67)" src="https://github.com/user-attachments/assets/d8167f3c-c22e-443d-adb7-fd7aad88e8f7" />


### Paso 5

Una vez ya abierto nos aparecera una ventana de bienvenida para la instalción y solo precionatremos "next"

<img width="1920" height="1080" alt="Captura de pantalla (68)" src="https://github.com/user-attachments/assets/4f987469-d1ff-4ad6-b05a-6bc91e3a0ba4" />


### Paso 6

Una vez que le dimos next nos pasara a otro apartado donde nos pregunta en donde queremos que se descargue ("como recomendacion es mejor dejarlo tal y como lo esta dejandon el programa") y le daremos netx

<img width="1920" height="1080" alt="Captura de pantalla (69)" src="https://github.com/user-attachments/assets/38c233de-611d-47a5-abdc-a97fe789c304" />


### Paso 7

Una vez que ya le dimos netx, le daremos en el boton install comenzara la descarga de Blender tambien le daremos que si en la venta que se abrira que estamos aceptando que Blender agregue archivos en nuestra computadora

<img width="1920" height="1080" alt="Captura de pantalla (70)" src="https://github.com/user-attachments/assets/7af98777-104a-435e-bae5-87df27f45143" />

<img width="1920" height="1080" alt="Captura de pantalla (71)" src="https://github.com/user-attachments/assets/5f2b88a9-2f00-43c6-9a1e-1361af9e4eef" />


### Paso 8

Una vez ya instalado podremos abrir Blender y ahora ya podemos programar :)

<img width="1920" height="1080" alt="Captura de pantalla (72)" src="https://github.com/user-attachments/assets/be5a1684-783d-4790-8c1f-007ea88c3a20" />


# POLIGONO

### Paso 1

Como primer paso abriremos Blender y en el menu de arriba buscaremos donde diga scripts y le daremos click

<img width="1920" height="1080" alt="Captura de pantalla (72)" src="https://github.com/user-attachments/assets/78541043-2f02-4618-9ea2-fa797f6dc2d4" />


### Paso 2 

Una vez que le dimos click en scripts le damos click donde dice nuevo y empezamos a escribrir las siguientes librerias 

Antes de crear nada, el script prepara el terreno:
- import bpy, math: Importas la librería de Blender (bpy) para controlar el software y la de matemáticas para usar $\pi$, seno y coseno.
- bpy.ops.object.select_all(action='SELECT') y .delete(): Estas líneas borran todo lo que haya en tu escena actual (cubos, luces, cámaras). Es como limpiar el lienzo antes de pintar.

<img width="1920" height="1080" alt="Captura de pantalla (74)" src="https://github.com/user-attachments/assets/d320c352-7f3c-4172-b805-95038363228e" />

<img width="1920" height="1080" alt="Captura de pantalla (75)" src="https://github.com/user-attachments/assets/4676037d-737a-4d35-ba1f-86c8aed5e773" />

Codigo de las librerias utilizadas:
```
import bpy
import math
```

### Paso 3

Dentro de la función crear_poligono_2d, ocurren tres pasos administrativos vitales en Blender:

1. La Malla (malla): Es la estructura de datos pura (vértices y aristas) pero sin presencia física en la escena todavía.
2. El Objeto (objeto): Es el "contenedor" que tendrá un nombre y una posición en el mundo.
3. El Vínculo (link): Conectas el objeto a la colección de la escena para que sea visible en el visor 3D.
   
<img width="1920" height="1080" alt="Captura de pantalla (76)" src="https://github.com/user-attachments/assets/9295fb03-e896-4565-b23b-ec55c247215c" />

Codigo:

```
 def crear_poligono_2d(nombre, lados, radio):
     #crear una nueva malla y un nuevo objeto
     malla = bpy.data.meshes.new(nombre)
     objeto = bpy.data.objects.new(nombre, malla)
    
     #vincular el objeto a la escena actual
     bpy.context.collection.objects.link(objeto)
```
### Paso 4

Aquí es donde el script decide dónde va cada punto del hexágono. Utiliza Coordenadas Polares.
1. El Ángulo: Para un hexágono (6 lados), divide un círculo completo ($2\pi$ radianes o 360°) entre 6.
   - Iteración 0: $0°
   - Iteración 1: $60°
   - Iteración 2: $120° y así sucesivamente.
2. Trigonometría:
   - *x* = radio ⋅ *cos(angulo)*
   - *y* = radio ⋅ *sin(angulo)*
   - *z* = 0 (porque es un polígono plano).
**Cada punto calculado se guarda en la lista vertices.**

<img width="1920" height="1080" alt="Captura de pantalla (77)" src="https://github.com/user-attachments/assets/49287211-e618-4561-9e81-d34f24a37089" />


Codigo:
```
    vertices = []
     aristas = []
    
     #Calculo de vertices usando coordenadas polares a cartesianas 
     for i in range(lados):
         angulo = 2 * math.pi * i / lados
         x = radio * math.cos(angulo)
         y = radio * math.sin(angulo)
         vertices.append((x, y, 0)) # Z = 0 para mantenerlo en 2D
```

### Paso 5

Una vez que tienes los puntos flotando en el espacio, necesitas "unirlos con líneas". El segundo bucle hace esto:

- aristas.append((i, (i + 1) % lados)):
  - Une el vértice 0 con el 1.
  - El 1 con el 2...
  - El truco del módulo (%) hace que cuando llegue al último vértice (el 5), lo conecte vuelta con el primero (el 0), cerrando la figura.
  
 <img width="1920" height="1080" alt="Captura de pantalla (78)" src="https://github.com/user-attachments/assets/3b34df38-0ee6-4f62-8094-38f692d00273" />

 Codigo:
 ```
     #Definir las conexiones (aristas) entre los vertices 
     for i in range(lados):
        aristas.append((i, (i + 1) % lados))
 ```

### Paso 6
Finalmente, se le entregan los datos a Blender:

- malla.from_pydata(vertices, aristas, []): Esta función toma tus listas de coordenadas y conexiones y genera la geometría real. El tercer parámetro [] está vacío porque no estamos creando "caras" sólidas (NGons), solo el contorno.
- malla.update(): Refresca la malla para que Blender procese los cambios.
  
<img width="1920" height="1080" alt="Captura de pantalla (79)" src="https://github.com/user-attachments/assets/c4a7a192-74fe-41b4-b505-634fc8b57373" />

Codigo: 
```
    # Cargar los datos en la malla
     malla.from_pydata(vertices, aristas, [])
     malla.update()
```

### Paso 7

Estas dos líneas evitan ese caos:

1. bpy.ops.object.select_all(action='SELECT'):
   - bpy.ops: Significa "Blender Operations" (herramientas que usarías con el ratón).
   - Esta instrucción simula presionar la tecla 'A' en el teclado dentro de Blender: selecciona absolutamente todo lo que exista en la vista 3D (cubos, cámaras, luces).

2. bpy.ops.object.delete():
   - Simula presionar la tecla 'X' o 'Suprimir'. Borra todo lo que se seleccionó en el paso anterior.
   - Resultado: Te deja un lienzo totalmente en blanco (una escena vacía).
     
<img width="1920" height="1080" alt="Captura de pantalla (80)" src="https://github.com/user-attachments/assets/b280825f-f37b-445e-9f21-b79801e5d764" />

Codigo:

```
#Limpiar la escena antes de empezar
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```

### Paso 8

Aquí es donde realmente se crea la geometría usando la función que definiste arriba:
   - crear_poligono_2d("Poligono2D", lados=6, radio=5)

Al ejecutar esta línea, le envías tres parámetros (instrucciones) a tu función:
 1. "Poligono2D": Es el nombre que aparecerá en el listado de objetos (Outliner) a la derecha de tu pantalla en Blender.
 2. lados=6: Aquí defines la forma. Al ser 6, el cálculo matemático generará un hexágono. Si cambiaras este número a 3, obtendrías un triángulo; si fuera 8, un octágono.
 3. radio=5: Es el tamaño. Define qué tan lejos del centro (0,0,0) estarán los puntos. En este caso, el hexágono medirá 10 unidades de diámetro total (5 de radio hacia cada lado).

<img width="1920" height="1080" alt="Captura de pantalla (81)" src="https://github.com/user-attachments/assets/ba62faa4-a6ad-425c-b5c0-7ee26ce44d61" />

Codigo:

```
#Llamada a la funcion: Un hexagono de radio 5
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```
### Compilacion

Una vez ya terminado daremos click en el boton de ejecutar y aparecera nuestro programa ya compilado.

<img width="1920" height="1080" alt="Captura de pantalla (82)" src="https://github.com/user-attachments/assets/14c3ffd3-782f-4675-8699-17f2b19be5e4" />

Codigo completo:
```
import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
     #crear una nueva malla y un nuevo objeto
     malla = bpy.data.meshes.new(nombre)
     objeto = bpy.data.objects.new(nombre, malla)
    
     #vincular el objeto a la escena actual
     bpy.context.collection.objects.link(objeto)
    
     vertices = []
     aristas = []
    
     #Calculo de vertices usando coordenadas polares a cartesianas 
     for i in range(lados):
         angulo = 2 * math.pi * i / lados
         x = radio * math.cos(angulo)
         y = radio * math.sin(angulo)
         vertices.append((x, y, 0)) # Z = 0 para mantenerlo en 2D
        
     #Definir las conexiones (aristas) entre los vertices 
     for i in range(lados):
        aristas.append((i, (i + 1) % lados))
    
     # Cargar los datos en la malla
     malla.from_pydata(vertices, aristas, [])
     malla.update()
    
#Limpiar la escena antes de empezar
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
 
#Llamada a la funcion: Un hexagono de radio 5
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```
# FLOR DE VIDA 

### Paso 1
Como bien ya lo hemos echo antes abriremos scripts y le daremos en nuevo
y empezaremos poniendo nuestras librerias:
- import bpy: Importa la librería de Blender que permite controlar todas las funciones del programa (crear objetos, moverlos, etc.).

import math: Importa funciones matemáticas necesarias para usar senos, cosenos y convertir grados a radianes.

<img width="1920" height="1080" alt="Captura de pantalla (84)" src="https://github.com/user-attachments/assets/50bd8dda-118d-40ba-a6b4-be726951a096" />


```
import bpy
import math
```

### Paso 2
- bpy.ops.object.select_all(action='SELECT'): Selecciona todos los objetos que existan actualmente en la escena 3D.
- bpy.ops.object.delete(): Borra los objetos seleccionados. Esto asegura que cada vez que corras el script, la escena empiece limpia.

<img width="1920" height="1080" alt="Captura de pantalla (85)" src="https://github.com/user-attachments/assets/08a76b24-ff02-4312-850a-4e35f51bd7db" />

```
# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```

### Paso 3
- radio = 3: Define el tamaño de los círculos.
- angulo_actual = 0: Es el punto de partida (0 grados). Se usará para rotar alrededor del centro.
- paso_angular = 60: Define que cada círculo nuevo se colocará 60° después del anterior (360 / 6 = 60).
  
<img width="1920" height="1080" alt="Captura de pantalla (86)" src="https://github.com/user-attachments/assets/91655b6f-6e54-420a-907f-8250b6e5c64a" />

Codigo:
```
# Parámetros de la figura
radio = 3
angulo_actual = 0
paso_angular = 60 # Cada 60 grados para obtener 6 círculos alrededor
```

### Paso 4
- bpy.ops.mesh.primitive_circle_add(...): Esta línea crea el círculo central en las coordenadas (0, 0, 0).

<img width="1920" height="1080" alt="Captura de pantalla (87)" src="https://github.com/user-attachments/assets/4e6f976f-91da-482b-a93b-1bc4646e927a" />

Codigo:
```
# 1. Círculo Central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)
```

### Paso 5
Este ciclo se repite mientras angulo_actual sea menor a 360. Es decir, dará una vuelta completa:
- x = radio * math.cos(math.radians(angulo_actual)): Calcula la posición en el eje X. Como el radio de los círculos exteriores es el mismo que el central, la distancia al centro es igual al radio.
- y = radio * math.sin(math.radians(angulo_actual)): Calcula la posición en el eje Y usando trigonometría básica.
- bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64): Crea un círculo en la posición *(x, y)* calculada.
- angulo_actual += paso_angular: Suma 60 a la variable. Sin esto, el código se quedaría atrapado creando círculos en el mismo sitio para siempre (bucle infinito).

<img width="1920" height="1080" alt="Captura de pantalla (88)" src="https://github.com/user-attachments/assets/d4f8a1f5-7e65-47d8-bb09-56e8313664b1" />

Codigo:
```
# --- INICIO DEL PATRÓN REPETITIVO CON WHILE ---

# El ciclo debe ejecutarse mientras el angulo_actual sea menor a 360
while angulo_actual < 360:
    # 1. Calcular la nueva posición (x, y) usando el ángulo actual
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    
    # 2. Llamar a la función de Blender para añadir el círculo
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    
    # 3. Actualización de estado: Incrementar el ángulo para evitar bucle infinito
    angulo_actual += paso_angular
```

### Paso 6
- print("Patrón completado con éxito."): Muestra un mensaje en la consola de Blender confirmando que el script terminó de ejecutarse.
- 
<img width="1920" height="1080" alt="Captura de pantalla (89)" src="https://github.com/user-attachments/assets/00ed7395-c0bb-4803-9b00-277cd2fe4ba0" />

Codigo:
```
print("Patrón completado con éxito.")
```

# Ejecución del programa
Una vez ya terminado daremos click en el boton de ejecutar y aparecera nuestro programa ya !
compilado.

<img width="1920" height="1080" alt="Captura de pantalla (90)" src="https://github.com/user-attachments/assets/6da1e137-fc4f-4cc2-aa5f-519fe94bec2b" />

Codigo completo:
```
import bpy
import math

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros de la figura
radio = 3
angulo_actual = 0
paso_angular = 60 # Cada 60 grados para obtener 6 círculos alrededor

# 1. Círculo Central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

# --- INICIO DEL PATRÓN REPETITIVO CON WHILE ---

# El ciclo debe ejecutarse mientras el angulo_actual sea menor a 360
while angulo_actual < 360:
    # 1. Calcular la nueva posición (x, y) usando el ángulo actual
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    
    # 2. Llamar a la función de Blender para añadir el círculo
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    
    # 3. Actualización de estado: Incrementar el ángulo para evitar bucle infinito
    angulo_actual += paso_angular

print("Patrón completado con éxito.")
```
### Nota

Si queremos agregar mas circulos a la flor. 
Por ejemplo 20 tenemos que usar una formula matematica que conciste en esto:

Para cambiar la cantidad de círculos a 20, solo necesitas modificar una variable: el paso_angular.
La lógica es simple: una vuelta completa tiene 360 grados. Si quieres que 20 círculos se 
repartan equitativamente en esa vuelta, debes dividir 360 entre 20.

<img width="1920" height="1080" alt="Captura de pantalla (92)" src="https://github.com/user-attachments/assets/94b7bdad-f843-420f-a6fc-bae506b2e367" />

Codigo completo:
```
paso_angular = 18 # Cada 18 grados para obtener 20 círculos alrededor
```
