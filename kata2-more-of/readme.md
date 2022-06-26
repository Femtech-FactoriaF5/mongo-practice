## Library


Crear una bd “libreria” y cargar los scripts adjuntos con el comando `load("nombrefichero")` desde el __mongo shell__.

Lanzar las siguientes queries:


- Obtener todos los autores
  
    db.libros.aggregate(
    [
        {$group: {
 _id:{
   nombre: "$autor.nombre",
   apellidos: "$autor.apellidos"
 }
}}

    ]
    )
    

- Obtener los autores cuyo apellido sea DATE
  
    db.libros.aggregate(
    [
        {$match: {
  "autor.apellidos": "DATE"
}},
        {$project: {
  _id: "$autor"
}}
    ]
    )
    

- Obtener los libros editados en 1998 o en 2005
  
    
    db.libros.aggregate(
    [
        {$match: {
  $or:[{anyo:"1998"},{anyo:"2005"}]
}},
        {$project: {
  titulo: "$titulo",
  añoEdicion: "$anyo",
  _id: 0
}}
    ]
    )
    

- Obtener el número de libros de la editorial Addison‐Wesley
  
    db.libros.aggregate(
    [
        {$match: {
  
editorial:"Addison-Wesley"
}},
        {$count: 'editorial'}
    ]
    )
    


- Obtener el libro que ocupa la tercera posición
  
    db.libros.aggregate(
    [
        {$skip: 2},
        {$limit: 1},
        {$project: {
 titulo: "$titulo",
 _id: 0
}}

    ]
    )
    

- Obtener la lista de autores de cada libro junto con el título
db.libros.aggregate(
[
{$project: {
  titulo: "$titulo",
  nombre: "$autor.nombre",
  apellidos:"$autor.apellidos",
  _id:0
}}

]
)

- Obtener los títulos de libro publicados con posterioridad a 2004.
  
    db.libros.aggregate(
    [
        {$match: {
  anyo: {$gt:"2005"}
}},
        {$project:{
  titulo: "$titulo",
  _id:0
}}
    ]
    )
    

- Obtener los libros editados desde 2001 y precio mayor que 50
 db.libros.aggregate(
    [
        {$match: {
  $and: [{anyo: {$gte:"2001"}}, {precio: {$gt:50}}]
}},
        {$project:{
  titulo: "$titulo",
  _id:0
}}
    ]
    )

- Obtener los libros publicados por la editorial Addison‐Wesley después de 2005.
  
   db.libros.aggregate(
    [
        {$match: {
  $and: [{anyo: {$gt:"2005"}},{editorial:"Addison-Wesley"}]
}},
        {$project:{
  titulo: "$titulo",
  _id:0
}}
    ]
    )
    

- Obtener el título de libro y editorial para aquellos libros que tengan un precio superior a 50€.
    
     db.libros.aggregate(
    [
        {$match: {
  precio: {$gt:60}
}},
        {$project:{
  titulo: "$titulo",
  editorial: "$editorial",
  _id:0
}}
    ]
    )


- Obtener los libros publicados en 1998 o a partir de 2005.

      db.libros.aggregate(
    [
        {$match: {
  $or:[{anyo: {$gt:"2005"}},{anyo: "1998"}]
}},
        {$project:{
  titulo: "$titulo",
  _id:0
}}
    ]
    )
