# 培訓教程-遥感地理

Google Earth Engine NDVI Statistics for 龍環葡韻 (Coloane, Macau)
![主介面](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/AppPyNDVI0.png?raw=true)
```py
import ee
import geemap
# Trigger the authentication flow.
ee.Authenticate()
# Initialize the library.
ee.Initialize(project='prime-boulevard-180404')
# Initialize Earth Engine
print(ee.String('Hello from the Earth Engine servers!').getInfo())
# Define the area of interest (龍環葡韻 wetlands)
aoi = ee.Geometry.Polygon([
    [113.558, 22.125],
    [113.558, 22.122],
    [113.561, 22.122],
    [113.561, 22.125]
])
# Function to calculate NDVI
def add_ndvi(image):
    ndvi = image.normalizedDifference(['B8', 'B4']).rename('NDVI')
    return image.addBands(ndvi)

# Get Sentinel-2 imagery
collection = (ee.ImageCollection('COPERNICUS/S2_SR')
             .filterBounds(aoi)
             .filterDate('2023-01-01', '2023-12-31')
             .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
             .map(add_ndvi))

# Select the least cloudy image
image = collection.sort('CLOUDY_PIXEL_PERCENTAGE').first()

# Calculate NDVI statistics
stats = image.select('NDVI').reduceRegion(
    reducer=ee.Reducer.mean().combine(
        reducer2=ee.Reducer.stdDev(),
        sharedInputs=True
    ).combine(
        reducer2=ee.Reducer.minMax(),
        sharedInputs=True
    ),
    geometry=aoi,
    scale=10,
    maxPixels=1e9
)
# Print the numerical results
print('NDVI Statistics for 龍環葡韻:')
print('Mean NDVI:', stats.get('NDVI_mean').getInfo())
print('Std Dev:', stats.get('NDVI_stdDev').getInfo())
print('Min NDVI:', stats.get('NDVI_min').getInfo())
print('Max NDVI:', stats.get('NDVI_max').getInfo())
# Create and display an interactive map
Map = geemap.Map()
Map.centerObject(aoi, 15)
Map.addLayer(aoi, {'color': 'red'}, 'Study Area')
Map.addLayer(image, {'bands': ['B4', 'B3', 'B2'], 'min': 0, 'max': 3000}, 'RGB')
Map.addLayer(image.select('NDVI'), {'min': -1, 'max': 1, 'palette': ['red', 'yellow', 'green']}, 'NDVI')
Map.addLayerControl()
Map

```
![主介面](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/AppPyNDVI1.png?raw=true)

```js
// Define the area of interest (approximate coordinates for 龍環葡韻)
var lon = 113.558;
var lat = 22.123;
var poi = ee.Geometry.Point([lon, lat]);
var bufferDistance = 500; // meters
var aoi = poi.buffer(bufferDistance);

// Function to calculate NDVI from Sentinel-2
function addNDVI(image) {
  var ndvi = image.normalizedDifference(['B8', 'B4']).rename('NDVI');
  return image.addBands(ndvi);
}

// Load Sentinel-2 imagery
var collection = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterBounds(aoi)
  .filterDate('2020-01-01', '2023-12-31')
  .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 20))
  .map(addNDVI);

// Calculate mean NDVI for the AOI
var meanNdvi = collection.select('NDVI').mean();
var stats = meanNdvi.reduceRegion({
  reducer: ee.Reducer.mean(),
  geometry: aoi,
  scale: 10,
  maxPixels: 1e9
});

print('Mean NDVI for 龍環葡韻:', stats.get('NDVI'));

// For time series analysis
var chart = ui.Chart.image.seriesByRegion({
  imageCollection: collection.select('NDVI'),
  regions: aoi,
  reducer: ee.Reducer.mean(),
  scale: 10,
  xProperty: 'system:time_start'
}).setOptions({
  title: 'NDVI Time Series for 龍環葡韻',
  vAxis: {title: 'NDVI'},
  hAxis: {title: 'Date'}
});

print(chart);

// Display on map
Map.centerObject(aoi, 14);
Map.addLayer(aoi, {color: 'red'}, 'Area of Interest');
Map.addLayer(meanNdvi.clip(aoi), {min: 0, max: 1, palette: ['red', 'yellow', 'green']}, 'Mean NDVI');

```
