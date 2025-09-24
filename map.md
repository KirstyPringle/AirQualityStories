---
layout: default
title: Map
extra_head: |
<meta name="robots" content="index,follow">
---


<div id="map" aria-label="Stories map"></div>


<script>
// 1) Basic Leaflet map
const map = L.map('map').setView([20, 0], 2); // world view
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
maxZoom: 18,
attribution: '&copy; OpenStreetMap contributors'
}).addTo(map);


// 2) Load approved stories (GeoJSON)
fetch('{{ "/data/stories.geojson" | relative_url }}')
.then(r => r.json())
.then(geojson => {
const layer = L.geoJSON(geojson, {
pointToLayer: (feature, latlng) => L.circleMarker(latlng, { radius: 6 }),
onEachFeature: (feature, layer) => {
const p = feature.properties || {};
const date = p.date || '';
const name = p.name || 'Anonymous';
const location = p.location || '';
const story = (p.story || '').replace(/\n/g,'<br>');
layer.bindPopup(
`<strong>${name}</strong><br>${date}${location ? ' — ' + location : ''}<br><br>${story}`
);
}
}).addTo(map);


// Fit bounds if we have points
try { map.fitBounds(layer.getBounds(), { padding: [20,20] }); } catch (e) {}
})
.catch(err => console.error('Failed to load stories:', err));
</script>
