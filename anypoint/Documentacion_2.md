# Continuación de lo realizado en el diseño de la API
## Después de las revisiones del 18 y 20 de Diciembre de 2023

## Uso de Traits

Para manejar de una manera más rápida los errores en la API, se hizo uso de los `Traits`. Similar a lo realizado con los `types` o los `examples`, se definió un archivo donde colocamos las respuestas 400, 404, etc. Después de eso, simplemente importamos el trait de forma similar a los `types` en el archivo principal. Seguido de eso, lo utilizamos en cada endpoint y con ello reducimos una gran cantidad de código.