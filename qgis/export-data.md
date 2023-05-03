# Export data

You can export all layers into your target folder as a geopackage

{% code overflow="wrap" %}
```python
myDir="path/of/target_folder"
layers = QgsProject.instance().mapLayers()
for layer_id, layer in layers.items():
    # Construct the file name for the output Geopackage file
    file_name = os.path.join(myDir, layer.name() + '.gpkg')
    # Save the layer as a Geopackage file
    QgsVectorFileWriter.writeAsVectorFormat(layer, file_name, 'utf-8', layer.crs(), 'GPKG')
    
```
{% endcode %}
