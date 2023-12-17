# Proceso de desarrollo de la API de entretenimiento
## API: Catálogo y reseñas de caricaturas

<div align="center">
    <img src="https://c4.wallpaperflare.com/wallpaper/242/145/84/patrick-star-nickelodeon-spongebob-squarepants-caricature-cartoons-colorful-wallpaper-preview.jpg" alt="imagen" width="500"/>
</div>

## Herramientas

- Draw.io
- Anypoint
- RAML

## Descripción de la API

Desarrollo de una API para un catálogo de caricaturas, con el cual se deben poder realizar las siguientes funciones:

- `Listado general:` Se debe tener un endpoint para enlistar todas las caricaturas que posee el catálogo.

- `Listado por género:` Se debe tener un endpoint para enlistar todas las caricaturas de un determinado género.

- `Obtener caricatura por título:` Se debe tener un endpoint para obtener una caricatura en base al título dado.

- `Listado por estudio de animación:` Se debe de tener un endpoint para enlistar todas las caricaturas de una determinada casa de animación.

- `Listado por creador/a:` Se debe de tener un endpoint para enlistar todas las caricaturas de un creador/a dado.

- `Crear una reseña:` Se debe de tener un endpoint para poder hacer una reseña y calificar una caricatura.

- `Obtener recomendaciones:` El usuario debe poder obtener recomendaciones personalizadas en base a las reseñas realizadas y los géneros que mejor califique.

En cuanto a los datos que la API debe retornar de cada caricatura deben ser los siguientes:

1. Título
2. Género
3. Sinopsis
4. Temporadas
5. Capítulos
6. Fecha de estreno
7. Estudio de animación
8. Creador/a
9. Calificación media
10. Portada

En caso de obtener solo una única caricatura, como es uno de los endpoints requeridos, también de manera adicional, debemos retornar las reseñas que esta posea con los siguientes datos:

1. Título
2. Portada
3. Usuario
4. Fecha
5. Reseña
6. Calificación
7. Spoiler

## Planeación de la API con Draw.io

Para tener una idea más clara y completa del desarrollo de la API, decidí crear una serie de diagramas en _**Draw.io**_, con los cuales también determiné con más claridad la información que deben contener las entidades que involucra el desarrollo de la API.

Simplemente para ver el diagrama, descargue el archivo de nombre `DiseñoAPI.drawio` y ábralo en la página web [Draw.io](https://app.diagrams.net/).

## <a href="./anypoint/Documentacion.md">🏭 Desarrollo de la API con Anypoint y RAML</a>
## <a href="./anypoint/Dudas.md">❔ Dudas</a>

> [!NOTE]
> Próximamente: Desarrollo de la API pero con Swagger y OpenAPI