# Diseñando la API en Anypoint

> [!IMPORTANT]
> Los códigos colocados aquí pueden diferir del resultado final en el RAML de anypoint.

Para comenzar con el diseño de la API, fui a la página de `Anypoint Platform` > `Design Center` > `Create` > `New API Specification`.

1. Comencé con el diseño de la API con cierta soltura, gracias al diseño previo realizado con _Draw.io_, empezando por la información básica del RAML.

```
#%RAML 1.0
title: Catálogo de caricaturas
version: v1
description: Una API para obtener información sobre diversas caricaturas asi como poder realizar reseñas a las mismas.
```

2. Seguido de eso, comencé con el endpoint para enlistar todas las caricaturas de la API.

```
/caricaturas:
  get:
    description: Obtener un listado de todos los cartoon de la API
    queryParameters:
      page:
        displayName: Página
        type: integer
        description: Número de página
        example: 1
        default: 1
      size:
        displayName: Tamaño de página
        type: integer
        description: Número de elementos por página
        example: 6
        default: 10
    responses:
      200:
        body:
          application/json:
            example:
              {
                "data_caricaturas": {
                  "caricatura": !include ./Caricatura.raml,
                  "ejemplos": [
                    {
                      "titulo": "Hilda",
                      "genero": "aventuras",
                      "sinopsis": "Sigue las aventuras de Hilda, una niña de cabello azul que se muda de su bosque encantado a la ciudad de Trolberg, donde hace nuevos amigos y conoce a criaturas mágicas",
                      "temporadas": 3,
                      "capitulos": 34,
                      "fecha_estreno": "2018-08-21",
                      "casa_animadora": "Mercury Filmworks",
                      "creador": "Luke Pearson",
                      "calificacion_med": 4.8
                    },
                    {
                      "titulo": "The Owl House",
                      "genero": "fantasía",
                      "sinopsis": "Sigue las aventuras de Luz, una adolescente que descubre un portal a un mundo mágico donde se hace amiga de una bruja rebelde y un adorable demonio",
                      "temporadas": 2,
                      "capitulos": 29,
                      "fecha_estreno": "2020-01-10",
                      "casa_animadora": "Disney Television Animation",
                      "creador": "Dana Terrace",
                      "calificacion_med": 4.7
                    },
                    // mas cartoons
                  ],
                  "pagina_actual": 1,
                  "total_paginas": 30,
                  "links": {
                    "siguiente": "/caricaturas/page=2&size=10",
                    "anterior": null
                  }
                },
                "success": true,
                "status": 200
              }
            type: object
      400:
        description: Bad Request
        body:
          application/json:
            example:
              {
                "error": {
                  "message": "La solicitud no es válida. Verifica los parámetros proporcionados.",
                },
                "success": false,
                "status": 400
              }
            type: object
      500:
        description: Internal Server Error
        body:
          application/json:
            example:
              {
                "error": {
                  "message": "Hubo un problema interno en el servidor. Intenta de nuevo más tarde.",
                },
                "success": false,
                "status": 500
              }
            type: object
```

En el camino, fui aprendiendo cómo se va construyendo el archivo RAML, ya sea para manejar los casos de `errores`, las `paginaciones` y la `validación de campos`.

Pero durante el proceso, me encontré con los `types`. Como se puede observar en los ejemplos de la respuesta 200, algo como:

```
"caricatura": !include ./Caricatura.raml,
```

Por ende, tengo creado otro archivo con el nombre `Caricatura.raml` que contiene lo siguiente:

```
#%RAML 1.0 ResourceType

types:
  Caricatura:
    properties:
      titulo: string
      genero: string
      sinopsis: string
      temporadas: number
      capitulos: number
      fecha_estreno: datetime
      calificacion_med: number
      casa_animadora: string
      creador: string
```

Mis dudas son:
1. ¿Está bien implementado?
2. ¿Cumple con lo que se supone que tiene que cumplir?
3. ¿Me pueden explicar más sobre los types?

Fuera de eso continué con el resto del diseño de la API sin mayores problemas