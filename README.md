# Procesamiento de datos de eBird
* Jupyter Notebook para obtención de los datos de eBird en un archivo CSV: [obtencion-datos-ebird.ipynb](https://github.com/biomonitoreo-participativo/procesamiento-datos-ebird/blob/master/obtencion-datos-ebird.ipynb)
* Jupyter Notebook para visualización de los datos de eBird en un archivo CSV: [visualizacion-datos-ebird.ipynb](https://github.com/biomonitoreo-participativo/procesamiento-datos-ebird/blob/master/visualizacion-datos-ebird.ipynb)

## Generación de cuadrículas de riqueza de especies
### Cuadrículas generadas a partir de la división político administrativa del IGN en el SNIT
Descarga de la capa de provincias
```terminal
# WGS84
$ ogr2ogr -t_srs EPSG:4326 cr_provincias_wgs84.shp WFS:"http://geos.snitcr.go.cr/be/IGN_5/wfs?" limiteprovincial_5k

# CRTM05
$ ogr2ogr -t_srs EPSG:5367 cr_provincias_crtm05.shp WFS:"http://geos.snitcr.go.cr/be/IGN_5/wfs?" limiteprovincial_5k
```

Con la versión en CRTM05, se generaron dos cuadrículas: una de 4 x 4 km2 y otra de 8 x 8 km2. Ambas se reproyectaron a WGS84 y se calculó la riqueza de especies con:
```terminal
# 4 x 4 km2
$ ogr2ogr cr_grid_8kx8k_spp_wgs84.shp cr_grid_8kx8k_wgs84.shp -dialect sqlite -sql "SELECT g8.geometry, Count(DISTINCT sciname) AS spp FROM cr_grid_8kx8k_wgs84 g8 LEFT JOIN 'observaciones_wgs84.shp'.observaciones_wgs84 o ON ST_CONTAINS(g8.geometry, o.geometry) GROUP BY g8.geometry"

# 8 x 8 km2
$ ogr2ogr cr_grid_4kx4k_spp_wgs84.shp cr_grid_4kx4k_wgs84.shp -dialect sqlite -sql "SELECT g4.geometry, Count(DISTINCT sciname) AS spp FROM cr_grid_4kx4k_wgs84 g4 LEFT JOIN 'observaciones_wgs84.shp'.observaciones_wgs84 o ON ST_CONTAINS(g4.geometry, o.geometry) GROUP BY g4.geometry"
```

### Cuadrículas proporcionadas por Sinac
Conversión a WGS84
```terminal
$ ogr2ogr -t_srs EPSG:4326 Cuadricula4x4_nacional_WGS84.shp Cuadricula4x4_nacional.shp
```
