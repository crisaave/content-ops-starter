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

Y para el caso particular de este problema, los datos de se puede extraer desde aca:

<https://docs.google.com/spreadsheets/d/1YUo-K9_79w55Nyk0tZihLzLBpsHY_Ij9/edit?usp=sharing&ouid=117160480656857669696&rtpof=true&sd=true>

Con dichos datos, se procede a construir el código en Phyton, usando Jupyter Notebook:

```
#Se importan las librerias necesarias
```

```
#Se leen los archivos de Excel (los archivos estan en el mismo directorio que el de este JupyterNotebook)
```

```
#Función para calcular la distancia entre dos ciudades
def calcular_distancia(coord1, coord2):
return np.sqrt((coord1[0] - coord2[0])**2 + (coord1[1] - coord2[1])**2)
```

```
#Crear la matriz de distancias
```

```
#Crossover
```

```
fill_index = (punto2) % num_ciudades  # Comenzar en el final del segmento copiado
for ciudad in padre2:
    if ciudad not in hijo:
        while hijo[fill_index] != -1:
            fill_index = (fill_index + 1) % num_ciudades
        hijo[fill_index] = ciudad

return hijo


```

```
#Algoritmo Genético
```

```
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


```

La mejor ruta encontrada: \[13, 2, 3, 4, 6, 12, 7, 10, 9, 8, 0, 1, 11, 5]
Longitud total de la ruta: 34.91049160183179

Para acced

![](/images/ruta_viajero.jpg)

Nam rutrum magna sed pellentesque lobortis. Etiam quam mauris, iaculis eget ex ac, rutrum scelerisque nisl. Cras finibus dictum ex sed tincidunt. Morbi facilisis neque porta, blandit mauris quis, pharetra odio. Aliquam dictum quam quis elit auctor, at vestibulum ex pulvinar. Quisque lobortis a lectus quis faucibus. Nulla vitae pellentesque nibh, et fringilla erat. Praesent placerat ac est at tincidunt. Praesent ultricies a ex at ultrices. Etiam sed tincidunt elit. Nulla sagittis neque neque, ultrices dignissim sapien pellentesque faucibus. Donec tempor orci sed consectetur dictum. Ut viverra ut enim ac semper. Integer lacinia sem in arcu tempor faucibus eget non urna. Praesent vel nunc eu libero aliquet interdum non vitae elit. Maecenas pharetra ipsum dolor, et iaculis elit ornare ac.
