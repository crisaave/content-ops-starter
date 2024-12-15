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
Dado una serie de n nodos y distancias para cada par de nodos, la idea es encontrar un viaje de ida y vuelta que tome la menor distancia pero que visite cada nodo exactamente una sola vez (ojo que la distancia del nodo i al j es la misma que del j al i).

#### Dado una serie de n nodos y distancias para cada par de nodos, la idea es encontrar un viaje de ida y vuelta que tome la menor distancia pero que visite cada nodo exactamente una sola vez (ojo que la distancia del nodo i al j es la misma que del j al i).

.

> Basado en el libro Hands-On Genetcringilla. Pellentesque dapibus suscipit faucibus. Nullam malesuada sed urna quis rutrum. Donec facilisis lorem id maximus mattis. Vestibulum quis elit magna. Vestibulum accumsan blandit consequat. Phasellus quis posuere quam.
>
> *By Clara White - VP of Marketing*



Para acceder a a una serie de datos

http\://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/

<http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/>

En el caso particular de este problema, los datos de se puede extraer del link adjunto

<https://docs.google.com/spreadsheets/d/1YUo-K9_79w55Nyk0tZihLzLBpsHY_Ij9/edit?usp=sharing&ouid=117160480656857669696&rtpof=true&sd=true>

```
#Se importan las librerias necesarias
import pandas as pd
import random
import numpy as np
from matplotlib import pyplot as plt
```

```
#Se leen los archivos de Excel (los archivos estan en el mismo directorio que el de este JupyterNotebook)
df_stp = pd.read_excel('Ciudad Burma.xlsx')
```

```
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
```

ex. Nullam cursus, urna et dapibus aliquam, urna leo euismod metus, eu luctus justo mi eget mauris. Proin felis leo, volutpat et purus in, lacinia luctus teger vel convallis justo.

![](/images/ruta_viajero.jpg)

Nam rutrum magna sed pellentesque lobortis. Etiam quam mauris, iaculis eget ex ac, rutrum scelerisque nisl. Cras finibus dictum ex sed tincidunt. Morbi facilisis neque porta, blandit mauris quis, pharetra odio. Aliquam dictum quam quis elit auctor, at vestibulum ex pulvinar. Quisque lobortis a lectus quis faucibus. Nulla vitae pellentesque nibh, et fringilla erat. Praesent placerat ac est at tincidunt. Praesent ultricies a ex at ultrices. Etiam sed tincidunt elit. Nulla sagittis neque neque, ultrices dignissim sapien pellentesque faucibus. Donec tempor orci sed consectetur dictum. Ut viverra ut enim ac semper. Integer lacinia sem in arcu tempor faucibus eget non urna. Praesent vel nunc eu libero aliquet interdum non vitae elit. Maecenas pharetra ipsum dolor, et iaculis elit ornare ac.
