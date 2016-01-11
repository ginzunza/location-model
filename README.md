# location-model
Un breve ejemplo sobre cómo crear países, regiones,provincias y ciudades, dado un modelo "Location". Cabe destacar que los ejemplos irán enfocados al país Chile.
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
Dentro de la Clase Location, se tienen las siguientes asociaciones:
```ruby
class Location < ActiveRecord::Base
  # associations
  belongs_to :parent_location, class_name: 'Location'
  has_many :locations, foreign_key: 'parent_location_id'
end
```
#Creando Países
Lo primero que se debe crear, para mantener la consistencia entre las relaciones que habrán más adelante, son los países. La única diferencia que poseerá, respecto a las otras tablas, será que el atributo "parent_location_id" será Nil. Dicho eso, para la creación se debe utilizar la siguiente sintaxis:
```ruby
Location.create(name:"Chile")
```
#Creando Regiones
Una vez creado el o los países se podrán crear las regiones. Cabe destacar que también se pueden crear regiones sin la existencia de países, pero será necesario hacer las relaciones más adelante. El código para la creación de una región, siguiendo el ejemplo anterior, es el siguiente:
```ruby
#igualamos la variable "p" a la Location de Chile
p = Location.find_by_name "Chile"
#a Chile le asignamos una región
p.locations<< Location.new(name: "BíoBío")
```
#Creando Provincias
Luego de tener un país y una región, creamos una provincia con el siguiente código:
```ruby
#primero igualamos la variable r a la región
r = Location.find_by_name "BíoBío"
r.locations<< Location.new(name: "Concepción")
```
#Obteniendo el nombre del padre
Una vez creado un País, su región y provincia, resulta útil saber cómo acceder al nombre del padre o, en otras palabras, es necesario saber a cuál región pertenece cada provincia o a cuál país pertenece cada región. Para ésto, el código que nos permite obtener esta información, es el siguiente:
```ruby
#igualamos la variable "c" a la Location en cuestión
c = Location.find_by_name "Concepción"
#Luego, para obtener el nombre de su región
Location.find(c.parent_location_id).name
#Para obtener el nombre del país de la región, se puede hacer lo siguiente
r = Location.find(c.parent_location_id)
#Después de igualar "r" a la región, aplicamos el mismo código, el cual nos dará el nombre del país
Location.find(r.parent_location_id).name

```
