# location-model
Un breve ejemplo sobre cómo crear Países, provincias y ciudades, dado un modelo "Location". Cabe destacar que los ejemplos irán enfocados al país Chile.
# Modelo Location
Se tiene el siguiente modelo en rails:<br />
```ruby
Location
{
  :id => nil,
  :name => nil,
  :parent_location_id => nil
}
```

#Creando Países
Lo primero que se debe crear, para mantener la consistencia entre las relaciones que habrán más adelante, son los países. La única diferencia que poseerá, respecto a las otras tablas, será que el atributo "parent_location_id" será Nil. Dicho eso, para la creación se debe utilizar la siguiente sintaxis:
```ruby
Location.create(name:"Chile")
```
#Creando Provincias
Una vez creado el o los países se podrán crear las provincias. Cabe destacar que también se pueden crear provincias sin la existencia de países, pero será necesario hacer las relaciones más adelante. El código para la creación de una provincia, siguiendo el ejemplo anterior, es el siguiente:
```ruby
#igualamos la variable "p" a la Location de Chile
p = Location.find_by_name "Chile"
#a Chile le asignamos una provincia
p.locations<< Location.new(name: "BíoBío")
```
#Creando Ciudades
Luego de tener un país y una provincia, creamos una ciudad con el siguiente código:
```ruby
#primero igualamos la variable p a la provincia
p = Location.find_by_name "BíoBío"
p.locations<< Location.new(name: "Concepción")
```
#Obteniendo el nombre del padre
Una vez creado un País, su provincia y una ciudad de la provincia, resulta útil saber cómo acceder al nombre del padre o, en otras palabras, es necesario saber a cuál provincia pertenece cada ciudad o a cuál país pertenece cada provincia. Para ésto, el código que nos permite obtener esta información es el siguiente:
```ruby
#igualamos la variable "c" a la Location en cuestión
c = Location.find_by_name "Concepción"
#Luego, para obtener el nombre de su provincia
Location.find(c.parent_location_id).name
#Para obtener el nombre del país de la provincia, se puede hacer lo siguiente
p = Location.find(c.parent_location_id)
#Después de igualar "p" a la provincia, aplicamos el mismo código, el cual nos dará el nombre del país
Location.find(p.parent_location_id).name

```
