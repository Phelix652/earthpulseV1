# EarthPulse V1

EarthPulse is a real-time global monitoring dashboard for earthquakes, flood events, weather, rain and wind, with location-based river discharge and marine conditions. It is designed for a static Netlify site plus Netlify serverless functions.

## What is live in V1

- Earthquakes: USGS Earthquake Catalog / GeoJSON and FDSN query service.
- Flood events: GDACS flood event feed (`FL`). These are event records, not a pixel-by-pixel flood map.
- Weather: Open-Meteo current + 3-day forecast at a selected coordinate.
- Rain + wind: Open-Meteo global model snapshot sampled on a coarse grid to keep the public app practical.
- River flood context: Open-Meteo Global Flood API backed by GloFAS data, queried at the selected location.
- Marine context: Open-Meteo Marine API for sea level including tides, waves and ocean currents at the selected location.
- Geocoding: Open-Meteo geocoding API.

## Data interpretation

This is a monitoring dashboard, not an official emergency-warning service. `Monitoring indicators` in the UI are project-defined thresholds intended to surface conditions for attention; they are not agency warnings.

The flood layer is intentionally labeled as **Flood events** because GDACS event records are not the same thing as a satellite flood-extent raster. The selected-location river discharge is also a model output. Local gauges and official authorities should be used for decisions.

NASA's near-real-time global flood products (MODIS MCDWD and VIIRS VCDWD) are intentionally not queried directly in this V1 browser layer because their best use is as imagery/product layers through NASA Worldview/GIBS, while raw NRT file access has authentication requirements. A V2 can add the NASA GIBS flood imagery layer without pretending it is a point-event feed.

## Folder structure

```text
EarthPulse/
├─ index.html
├─ netlify.toml
├─ package.json
├─ README.md
├─ DATA_SOURCES.md
└─ netlify/
   └─ functions/
      ├─ _lib.mjs
      ├─ health.mjs
      ├─ earthquakes.mjs
      ├─ flood-events.mjs
      ├─ geocode.mjs
      ├─ location.mjs
      └─ global-weather.mjs
```

## Deploy to Netlify

1. Put the project in GitHub.
2. In Netlify, create a site from the repository.
3. Build command: leave empty.
4. Publish directory: `.`
5. Functions directory is already configured as `netlify/functions` in `netlify.toml`.
6. Deploy.

No API keys are required for this V1.

## Production notes

### Map tiles
The V1 map uses the public OpenStreetMap standard raster tile endpoint. Keep traffic modest and review the current OSM tile usage policy before operating at high public volume. For a large production audience, replace the tile source with a dedicated hosted tile provider and its required key/attribution.

### Netlify functions
The functions use the modern fetch-style Netlify handler and native Node `fetch`. Netlify builds the functions with esbuild.

### Caching
The endpoints send short public cache headers to avoid hammering upstream scientific APIs. The browser polls earthquakes every 5 minutes, flood events every 15 minutes, and the global weather grid every 15 minutes.

### Error behavior
If one upstream service fails, the UI keeps the other layers alive and marks the failed feed in the status box. The app does not invent replacement hazard data.

## Suggested V2

- NASA GIBS near-real-time MODIS/VIIRS flood imagery as a raster overlay.
- Regional official warning feeds (for example CAP / national meteorological agencies) with clear country attribution.
- NOAA / regional tide-gauge observations where supported.
- Tropical cyclone tracks and wildfire detections.
- User-selected location alert subscriptions.
- Persistent event history and time slider.
