# Procesamiento de datos de eBird

* Jupyter Notebook para obtención de los datos de eBird en un archivo CSV: [obtencion-datos-ebird.ipynb](https://github.com/biomonitoreo-participativo/procesamiento-datos-ebird/blob/master/obtencion-datos-ebird.ipynb)
* Jupyter Notebook para visualización de los datos de eBird en un archivo CSV: [visualizacion-datos-ebird.ipynb](https://github.com/biomonitoreo-participativo/procesamiento-datos-ebird/blob/master/visualizacion-datos-ebird.ipynb)

Descarga de la capa de provincias
```terminal
# WGS84
$ ogr2ogr -t_srs EPSG:4326 cr_provincias_wgs84.shp WFS:"http://geos.snitcr.go.cr/be/IGN_5/wfs?" limiteprovincial_5k

# CRTM05
$ ogr2ogr -t_srs EPSG:5367 cr_provincias_crtm05.shp WFS:"http://geos.snitcr.go.cr/be/IGN_5/wfs?" limiteprovincial_5k
```
