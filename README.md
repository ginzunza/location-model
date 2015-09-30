# location-model
Un breve ejemplo sobre cómo crear Países, provincias y ciudades, dado un modelo "Location"
# Modelo Location
Se tiene el siguiente modelo en rails:<br />
Location<br />
{<br />
  :id => nil,<br />
  :name => nil,<br />
  :parent_location_id => nil<br />
}

#Creando Países
Lo primero que se debe crear, para mantener la consistencia entre las relaciones que hay en países, provincias y ciudades, son los países. La única diferencia que poseerá 
