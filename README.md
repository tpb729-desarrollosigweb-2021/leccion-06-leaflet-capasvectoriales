# Leaflet - capas vectoriales
[Leaflet](https://leafletjs.com/) puede manejar tanto capas vectoriales como raster. Aquí se describe el manejo de datos vectoriales mediante la clase GeoJSON.

## Clases del API de Leaflet

### Clase GeoJSON
La clase [GeoJSON](https://leafletjs.com/reference-1.7.1.html#geojson) representa un objeto o un arreglo de objetos GeoJSON, permitiendo su despliegue en un mapa Leaflet.

## Ejemplo de mapa Leaflet con capas vectoriales
Haga clic en la imagen para acceder al mapa interactivo.

[![[Código fuente]()](img/ejemplo-mapa-leaflet-capas-vectoriales.png)](https://tpb729-desarrollosigweb-2021.github.io/ejemplo-mapa-leaflet-capas-vectoriales/)

Código HTML, CSS y JavaScript

HTML
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Ejemplo de mapa desarrollado con Leaflet</title>     

    <!-- Enlace a biblioteca JQuery -->
    <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
    
    <!-- Enlace a hoja CSS de Leaflet -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A==" crossorigin=""/>
    
    <!-- Enlace a biblioteca JavaScript de Leaflet -->
    <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js" integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA==" crossorigin=""></script>    

    <link rel="stylesheet" href="css/estilos.css">
</head>
<body>
    <h1>Ejemplo de mapa Leaflet con capas vectoriales</h1>     
    
    <!-- Elemento div para contener el mapa Leaflet -->
    <div id="mapid"></div>

    <!-- Código JavaScript para generar y manejar el mapa Leaflet -->
    <script src="js/scripts.js"></script>					
</body>
</html>	
```

CSS
```css
#mapid { 
  height: 500px;
  width: 500px;
}
```

JavaScript
```javascript
// Mapa Leaflet
var mapa = L.map('mapid').setView([9.8, -84.25], 8);

// Definición de capas base
var capa_osm = L.tileLayer(
  'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png?', 
  {
    maxZoom: 19,
	attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }
).addTo(mapa);	

// Conjunto de capas base
var capas_base = {
  "OSM": capa_osm
};	    
	    
// Control de capas
control_capas = L.control.layers(capas_base).addTo(mapa);	

// Control de escala
L.control.scale().addTo(mapa);

// Capa vectorial en formato GeoJSON
$.getJSON("https://tpb729-desarrollosigweb-2021.github.io/datos/sinac/areas_protegidas-wgs84.geojson", function(geodata) {
  var capa_asp = L.geoJson(geodata, {
    style: function(feature) {
	  return {'color': "#013220", 'weight': 2.5, 'fillOpacity': 0.0}
    },
    onEachFeature: function(feature, layer) {
      var popupText = "<strong>Área protegida</strong>: " + feature.properties.nombre_asp + "<br>" + "<strong>Categoría</strong>: " + feature.properties.cat_manejo;
      layer.bindPopup(popupText);
    }			
  }).addTo(mapa);

  control_capas.addOverlay(capa_asp, 'Áreas protegidas');
});	
```

## La biblioteca jQuery
[jQuery](https://jquery.com/) es una biblioteca JavaScript de uso muy extendido. Fue diseñada para facilitar el acceso al [Document Object Model (DOM)](https://es.wikipedia.org/wiki/Document_Object_Model) de HTML, así como para el manejo de eventos y animaciones CSS, entre otras capacidades.

Para utilizar jQuery, debe incluirse su enlace en el documento HTML:
```html
// Enlace a jQuery
<script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>	
```

jQuery define una función global llamada ```jQuery()```, la cual acostumbra referenciarse de manera abreviada con el símbolo ```$```. La sintaxis básica de jQuery es ```$(selector).accion()```.

```javascript
// Esconde todos los elementos p
$("p").hide()

// Esconde todos los elementos de la clase test
$(".test").hide()

// Esconde el elemento con id="test"
$("#test").hide()

// Cambia el color de todos los elementos h1
$("h1").css("color", "#0088ff");
```
