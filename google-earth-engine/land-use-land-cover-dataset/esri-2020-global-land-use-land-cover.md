---
description: source:https://gee-community-catalog.org/projects/esrilc2020/
---

# ESRI 2020 Global Land Use Land Cover

This layer displays a global map of land use/land cover (LULC). The map is derived from ESA Sentinel-2 imagery at 10m resolution. It is a composite of LULC predictions for 10 classes throughout the year in order to generate a representative snapshot of 2020. This map was produced by a deep learning model trained using over 5 billion hand-labeled Sentinel-2 pixels, sampled from over 20,000 sites distributed across all major biomes of the world.

<pre class="language-javascript"><code class="lang-javascript">// Some code
// Define a dictionary which will be used to make legend and visualize image on map
var dict = {
  "names": [
    "Water",
    "Trees",
    "Grass",
    "Flooded Vegetation",
    "Crops",
    "Scrub/Shrub",
    "Built Area",
    "Bare Ground",
    "Snow/Ice",
    "Clouds"
  ],
  "colors": [
    "#1A5BAB",
    "#358221",
    "#A7D282",
    "#87D19E",
    "#FFDB5C",
    "#EECFA8",
    "#ED022A",
    "#EDE9E4",
    "#F2FAFF",
    "#C8C8C8"
  ]};
<strong>
</strong>var geometry = 
    ee.Geometry.Polygon(
        [[[12.329698441066297, 42.001473247131784],
          [12.329698441066297, 41.72328368979682],
          [12.906480667628797, 41.72328368979682],
          [12.906480667628797, 42.001473247131784]]], null, false);



var esri_lulc2020= ee.ImageCollection("projects/sat-io/open-datasets/landcover/ESRI_Global-LULC_10m")
var esri_mosaic = esri_lulc2020.mosaic()
var crop_esri = esri_mosaic.clip(geometry )
Map.addLayer(crop_esri, {min:1, max:10, palette:dict['colors']}, 'ESRI LULC 10m')
print(crop_esri)

Map.addLayer(image, {min:1, max:10, palette:dict['colors']}, 'image')
print(image)


var projection = crop_esri.projection().getInfo();
print(projection)
print(projection.crs)


Export.image.toAsset({
  image: crop_esri,
  description: 'esri_lulc_kochi_asset',
  assetId: 'esri_lulc_kochi',  // &#x3C;> modify these
  region: geometry ,
});


Export.image.toDrive({
  image: crop_esri,
  description: 'esri_lulc_kochi_toDrive',
  folder:'gee',
  //crs: projection.crs,
  //crsTransform: projection.transform,
  region: geometry ,
  scale: 10,
  maxPixels: 1e13,
  fileFormat: 'GeoTIFF',
});
Map.centerObject(crop_esri)

</code></pre>
