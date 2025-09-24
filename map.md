---
layout: default
title: "Map"
extra_head: |
  <meta name="robots" content="index,follow">
---

<div id="map" aria-label="Stories map"></div>

<script>
// 1) Make sure Leaflet exists
if (typeof L === "undefined") {
  console.error("Leaflet failed to load. Check _layouts/default.html script tag.");
}

// 2) Basic map
const map = L.map('map').setView([20, 0], 2);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  maxZoom: 18,
  attribution: '&copy; OpenStreetMap contributors'
}).addTo(map);

// 3) TEMP sanity marker (remove after testing)
L.marker([55.9533, -3.1883]).addTo(map).bindPopup("Leaflet is working!");

// 4) Load approved stories
fetch('{{ "/data/stories.geojson" | relative_url }}', { cache: "no-cache" })
  .then(r => {
    if (!r.ok) throw new Error("HTTP " + r.status + " loading stories.geojson");
    return r.json();
  })
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

    try { map.fitBounds(layer.getBounds(), { padding: [20,20] }); } catch (_) {}
  })
  .catch(err => {
    console.warn("Could not load stories.geojson:", err);
  });
</script>
