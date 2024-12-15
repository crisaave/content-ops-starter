---
title: Salesman Travel Problem con Algoritmo Genético
slug: case-study-1
date: '2024-12-15'
excerpt: >-
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ante lorem,
  tincidunt ac leo efficitur, feugiat tempor odio. Curabitur at auctor sapien.
  Etiam at cursus enim. Suspendisse sed augue tortor. Nunc eu magna vitae lorem
  pellentesque fermentum. Sed in facilisis dui.
featuredImage:
  url: /images/ruta_viajero.jpg
  altText: Case study 1
  styles:
    self:
      borderRadius: large
  type: ImageBlock
bottomSections:
  - title: Divider
    colors: bg-light-fg-dark
    styles:
      self:
        padding:
          - pt-7
          - pl-7
          - pb-7
          - pr-7
    type: DividerSection
  - items:
      - title: About Company
        tagline: This is the tagline
        subtitle: >-
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ante
          lorem, tincidunt ac leo efficitur, feugiat tempor odio. Curabitur at
          auctor sapien.
        image:
          url: /images/telus-logo.svg
          altText: Company logo
          styles:
            self:
              margin:
                - ml-3
          type: ImageBlock
        colors: bg-light-fg-dark
        styles:
          self:
            padding:
              - pt-6
              - pl-6
              - pb-6
              - pr-6
            textAlign: left
            borderColor: border-neutralAlt
            borderStyle: none
            borderWidth: 0
            borderRadius: none
            flexDirection: row
        type: FeaturedItem
    variant: small-list
    colors: bg-light-fg-dark
    styles:
      self:
        margin:
          - mb-20
        padding:
          - pt-0
          - pl-0
          - pb-0
          - pr-0
        justifyContent: center
      subtitle:
        textAlign: center
    type: FeaturedItemsSection
isFeatured: true
colors: bg-neutral-fg-dark
styles:
  self:
    padding:
      - pt-5
      - pl-5
      - pb-5
      - pr-5
    textAlign: center
    borderColor: border-light
    borderStyle: none
    borderWidth: 0
    borderRadius: none
    flexDirection: col
type: PostLayout
---
#### Dado una serie de n nodos y distancias para cada par de nodos, la idea es encontrar un viaje de ida y vuelta que tome la menor distancia, pero que visite cada nodo exactamente una sola vez (ojo que la distancia del nodo i al j es la misma que del j al i).

> Basado en el libro Hands-On Genetic Algorithms with Python
>
> *By Eyal Wirsansky - 2020 Packt Publishing*

Para acceder a datos de diversas ciudades, se recomienda el siguiente link:

[http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95](http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/)

Y para el caso particular de este problema (BURMA-MYANMAR), los datos de se puede extraer desde aca:

<https://docs.google.com/spreadsheets/d/1YUo-K9_79w55Nyk0tZihLzLBpsHY_Ij9/edit?usp=sharing&ouid=117160480656857669696&rtpof=true&sd=true>

Con dichos datos, se procede a construir el código en Phyton, usando Jupyter Notebook:

```
#Se importan las librerias necesarias
import pandas as pd
import random
import numpy as np
from matplotlib import pyplot as plt

#Se leen los archivos de Excel (los archivos estan en el mismo directorio que el de este JupyterNotebook)
df_stp = pd.read_excel('Ciudad Burma.xlsx')

#Función para calcular la distancia entre dos ciudades
def calcular_distancia(coord1, coord2):
return np.sqrt((coord1[0] - coord2[0])**2 + (coord1[1] - coord2[1])**2)
```

```
#Crear la matriz de distancias
num_ciudades = len(df_stp)
distancias = np.zeros((num_ciudades, num_ciudades))
for i in range(num_ciudades):
for j in range(num_ciudades):
if i != j:
coord1 = (df_stp['coord i'][i], df_stp['coord j'][i])
coord2 = (df_stp['coord i'][j], df_stp['coord j'][j])
distancias[i][j] = calcular_distancia(coord1, coord2)

#Calcular la longitud de la ruta
def calcular_longitud(ruta):
longitud_total = 0
for i in range(len(ruta)):
ciudad_actual = ruta[i]
ciudad_siguiente = ruta[(i + 1) % len(ruta)]  # Regresar a la primera ciudad al final
longitud_total += distancias[ciudad_actual][ciudad_siguiente]
return longitud_total
```

```
#Crear la población inicial
def crear_poblacion(tamano):
poblacion = []
for _ in range(tamano):
ruta = list(range(num_ciudades))  # Rutas que incluyen todas las ciudades
random.shuffle(ruta)  # Mezcla las ciudades
poblacion.append(ruta)
return poblacion
```

```
#Seleccionar dos padres de la población
def seleccionar_padres(poblacion):
seleccionados = random.sample(poblacion, 2)
return seleccionados[0] if calcular_longitud(seleccionados[0]) < calcular_longitud(seleccionados[1]) else seleccionados[1]
```

```
#Crossover
def order_crossover(padre1, padre2):
punto1, punto2 = sorted(random.sample(range(num_ciudades), 2))
hijo = [-1] * num_ciudades
hijo[punto1:punto2] = padre1[punto1:punto2]
fill_index = (punto2) % num_ciudades  # Comenzar en el final del segmento copiado
for ciudad in padre2:
    if ciudad not in hijo:
        while hijo[fill_index] != -1:
            fill_index = (fill_index + 1) % num_ciudades
        hijo[fill_index] = ciudad

return hijo

#Mutación
def mutar(ruta, tasa_mutacion=0.1):
for i in range(num_ciudades):
if random.random() < tasa_mutacion:
j = random.randint(0, num_ciudades - 1)
if i != j:  # Asegurarse de que no se intercambie la ciudad consigo misma
ruta[i], ruta[j] = ruta[j], ruta[i]
```

```
#Algoritmo Genético
def algoritmo_genetico(tamano_poblacion=100, generaciones=500):
poblacion = crear_poblacion(tamano_poblacion)
mejor_ruta = None
mejor_longitud = float('inf')
for _ in range(generaciones):
    nueva_poblacion = []

    for _ in range(tamano_poblacion):
        padre1 = seleccionar_padres(poblacion)
        padre2 = seleccionar_padres(poblacion)
        hijo = order_crossover(padre1, padre2)
        mutar(hijo)
        nueva_poblacion.append(hijo)

    poblacion = nueva_poblacion

    # Evaluar la nueva población
    for ruta in poblacion:
        longitud = calcular_longitud(ruta)
        if longitud < mejor_longitud:
            mejor_longitud = longitud
            mejor_ruta = ruta

return mejor_ruta, mejor_longitud

#Ejecutar el algoritmo genético
mejor_ruta, longitud_total = algoritmo_genetico(tamano_poblacion=100, generaciones=500)
print(f"La mejor ruta encontrada: {mejor_ruta}")
print(f"Longitud total de la ruta: {longitud_total}")
```

En este caso particular, la secuencia de ciudades recomendada por el programa es la siguiente : \[13, 2, 3, 4, 6, 12, 7, 10, 9, 8, 0, 1, 11, 5]
Y su longitud total recorrida es de 34.91

De forma grafica, se puede ver dicha secuencia, indicando la ciudad de inicio del viaje (ciudad 13) y su posterior camino hasta llegar el fin del recorrido (ciudad 5).

```
#Visualizar la ruta
def visualizar_ruta(ruta):
coords = df_stp[['coord i', 'coord j']].values
ruta_coords = coords[ruta]
plt.figure(figsize=(10, 6))
plt.plot(ruta_coords[:, 0], ruta_coords[:, 1], marker='o', linestyle='-', color='b')

#Etiquetas de las ciudades
for i, (x, y) in enumerate(zip(ruta_coords[:, 0], ruta_coords[:, 1])):
    plt.text(x, y, str(ruta[i]), fontsize=12, ha='center', va='bottom')  # Añade el número de ciudad centrado y ajustado verticalmente

#Etiqueta para el punto de partida
plt.text(ruta_coords[0, 0], ruta_coords[0, 1], 'Inicio', fontsize=12, ha='right', color='green')

#Etiqueta para el punto de llegada
plt.text(ruta_coords[-1, 0], ruta_coords[-1, 1], 'Fin', fontsize=12, ha='right', color='red')
plt.title("Ruta del Viajero")
plt.xlabel("Coordenada X")
plt.ylabel("Coordenada Y")
plt.grid()

#Guarda el grfico como archivo JPEG
plt.savefig(filename, format="jpg")  # Guarda el gráfico en formato .jpg o .jpeg
plt.show()
```

```
#Visualizar la mejor ruta
visualizar_ruta(mejor_ruta)
```

![](/images/ruta_viajero.jpg)
