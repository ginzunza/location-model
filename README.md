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
