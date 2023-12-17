# Diseñando la API en Anypoint

> [!NOTE]
> Dicha API esta publicada en anypoint con el nombre de Catalogo_Caricaturas

Para comenzar con el diseño de la API, fui a la página de `Anypoint Platform` > `Design Center` > `Create` > `New API Specification`.

Comencé con el diseño de la API con cierta soltura, gracias al diseño previo realizado con _Draw.io_, empezando por la información básica del RAML.

```
#%RAML 1.0
title: Catálogo de caricaturas
version: v1
description: Una API para obtener información sobre diversas caricaturas asi como poder realizar reseñas a las mismas.
```

Seguido de eso, comencé con el endpoint para enlistar todas las caricaturas de la API.

```
/caricaturas:
  get:
    displayName: GET All Cartoons
    description: Retorna una lista con todas las caricaturas presentes en el catálogo
    responses:
      200:
        body:
          application/json:
            type: Caricatura[]
            example: !include examples/caricaturasExample.raml
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

En el camino, fui aprendiendo cómo se va construyendo el archivo RAML, ya sea para manejar los casos de `errores`, las `paginaciones`, la `validación de campos`, `types` y los `examples`.

Como mencioné antes, hice uso de los `types`, los cuales ayudan a definir la estructura y tipos de datos que deben tener las respuestas. Para ello, creé uno para cada una de las entidades que había contemplado con anterioridad:

```
#%RAML 1.0 DataType
displayName: Caricatura
description: Define el tipo de datos de Caricatura

type: object
properties:
  id: number
  portada: string
  titulo: string
  genero: string
  sinopsis: string
  temporadas: number
  capitulos: number
  fecha_estreno: string
  casa_animadora: string
  creador: string
  calificacion_med: number
  resenas?: Resena[] 
```

Simplemente se importan en el archivo principal para hacer uso de estos:

```
types:
  Caricatura: !include data-types/caricaturaType.raml
  Resena: !include data-types/resenaType.raml
  Usuario: !include data-types/usuarioType.raml
```

Así también hice uso de los `examples` que son para dar como su nombre indica ejemplos de respuestas:

```
#%RAML 1.0 NamedExample
value:
-
  id: 8
  portada: "ruta/imagen.png"
  titulo: "El laboratorio de Dexter"
  genero: "comedia"
  sinopsis: "Sigue las aventuras de Dexter, un niño genio que tiene su propio laboratorio secreto, donde crea increíbles inventos que a menudo le causan problemas con su hermana mayor Dee Dee y otros personajes"
  temporadas: 4
  capitulos: 78
  fecha_estreno: "1996-04-28"
  casa_animadora: "Cartoon Network Studios"
  creador: "Genndy Tartakovsky"
  calificacion_med: 4.4
-
  id: 9
  portada: "ruta/imagen.png"
  titulo: "Primal"
  genero: "aventuras"
  sinopsis: "Sigue las aventuras de un cavernícola y un tiranosaurio que se unen para sobrevivir en un mundo prehistórico hostil y violento, donde la muerte acecha en cada esquina"
  temporadas: 2
  capitulos: 15
  fecha_estreno: "2019-10-07"
  casa_animadora: "Cartoon Network Studios"
  creador: "Genndy Tartakovsky"
  calificacion_med: 4.8
```

Haciendo que el código presente en el archivo principal sea más limpio y fácil de leer, simplemente para terminar, continué el diseño de la API sin mayores cambios o problemas.

## Bonus:

```
/agregarResena:
  post:
    displayName: ADD a Review
    description: Crea una nueva reseña para alguna caricatura en específico
    headers:
      Requester-ID:
        displayName: Requestor ID
        description: ID de la persona que está haciendo el request de los datos
        type: string
        required: true
      Authorization:
        displayName: Authorization
        description: Token de autenticación del usuario
        type: string
        required: true
      Content-Type:
        displayName: Content-Type
        description: Formato del cuerpo de la solicitud
        type: string
        required: true
      Accept-Language:
        displayName: Accept-Language
        description: Idioma preferido del cliente para las respuestas
        type: string
      Timestamp:
        displayName: Timestamp
        description: Timestamp de la solicitud
        type: string
      Request-ID:
        displayName: Request-ID
        description: Identificador único de la solicitud
        type: string
```

**`Explicación del códgo`**:

1. **Requester-ID (ID del Solicitante):**

  - `Descripción`: Identificador de la persona que está realizando la solicitud de datos. Este puede ser un identificador único asignado al usuario o al dispositivo que está haciendo la solicitud.

  - `Uso`: Ayuda a identificar y rastrear quién está haciendo la solicitud. Puede ser útil para realizar análisis de uso o para vincular la solicitud a un usuario específico.

2. **Authorization (Autorización):**

  - `Descripción`: Token de autenticación del usuario que está haciendo la solicitud. Este encabezado es comúnmente utilizado para autenticar y autorizar a los usuarios antes de permitir el acceso a recursos protegidos.

  - `Uso`: Garantiza que la solicitud provenga de un usuario autenticado y autorizado. Protege la seguridad de la información y los recursos.

3. **Content-Type (Tipo de Contenido):**

  - `Descripción`: Indica el formato del cuerpo de la solicitud. Puede ser application/json, application/xml, etc.

  - `Uso`: Permite al servidor entender cómo interpretar y procesar el cuerpo de la solicitud. En el caso de /agregarResena, se espera que el cuerpo de la solicitud esté en el formato especificado por este encabezado.

4. Accept-Language (Aceptar Idioma):

  - `Descripción`: Indica el idioma preferido del cliente para las respuestas. Puede ser útil cuando la API admite contenido internacionalizado y puede responder en diferentes idiomas.

  - Uso: Permite al cliente especificar su preferencia de idioma para las respuestas. Si la API puede proporcionar respuestas en diferentes idiomas, puede utilizar este encabezado para ajustar el idioma de las respuestas.

5. Timestamp (Marca de Tiempo):

  - `Descripción`: Indica la marca de tiempo en la que se realizó la solicitud. Es útil para registrar cuándo ocurrió la solicitud.
  
  - `Tipo`: string (podría ser preferible usar un formato de fecha y hora específico, como ISO 8601)

  - `Uso`: Facilita el rastreo temporal de las solicitudes. Puede ser utilizado para realizar análisis de rendimiento o para solucionar problemas relacionados con el tiempo de respuesta.

6. Request-ID (ID de la Solicitud):

  - `Descripción`: Identificador único de la solicitud. Ayuda a rastrear y referenciar una solicitud específica.

  - `Uso`: Facilita la resolución de problemas y el seguimiento de las solicitudes. Puede ser útil para correlacionar registros en el servidor con solicitudes específicas.