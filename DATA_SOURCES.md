# EarthPulse V1 data sources

## USGS
https://earthquake.usgs.gov/earthquakes/feed/

Used for global earthquake event data through the USGS Earthquake Catalog/FDSN service.

## GDACS
https://www.gdacs.org/
https://www.gdacs.org/gdacsapi/swagger/index.html

Used for recent flood event records (`FL`). GDACS is a multi-hazard coordination system and asks applications to acknowledge its source.

## Open-Meteo weather
https://open-meteo.com/en/docs

Used for current weather, wind, gusts, precipitation, rain, pressure, cloud cover and short forecasts.

## Open-Meteo Global Flood API / GloFAS
https://open-meteo.com/en/docs/flood-api

Used for selected-location river discharge. The API uses GloFAS v4 by default and returns modelled daily discharge, not a local flood-gauge observation.

## Open-Meteo Marine
https://open-meteo.com/en/docs/marine-weather-api

Used for selected-location modelled sea level including tides, wave state and ocean currents. The provider explicitly notes that coastal accuracy can be limited and the data are not suitable for coastal navigation.

## NASA near-real-time global flood products
https://www.earthdata.nasa.gov/topics/human-dimensions/natural-hazards/floods
https://worldview.earthdata.nasa.gov/

NASA LANCE currently provides near-real-time MODIS and VIIRS global flood products. The products are around 250 m resolution, updated from polar-orbiting imagery, and are best treated as imagery/product layers with known optical/cloud limitations. V1 links the concept in documentation and reserves a direct NASA GIBS raster overlay for V2.

## Map
MapLibre GL JS: https://maplibre.org/maplibre-gl-js/docs/

Base map: OpenStreetMap standard tiles. This has attribution in the map.
