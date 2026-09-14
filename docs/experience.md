---
hide:
  - toc
  - navigation
---

# Experience & Education

A global overview of my professional engagements and applied research. Click any marker to view project specifics.

<!-- Leaflet & MarkerCluster CSS/JS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<link rel="stylesheet" href="https://unpkg.com/leaflet.markercluster@1.5.3/dist/MarkerCluster.css" />
<link rel="stylesheet" href="https://unpkg.com/leaflet.markercluster@1.5.3/dist/MarkerCluster.Default.css" />

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script src="https://unpkg.com/leaflet.markercluster@1.5.3/dist/leaflet.markercluster.js"></script>

<style>
  /* Custom Marker Style & Animation */
  .custom-map-marker {
    background-color: #00a884;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    border: 2px solid #ffffff;
    box-shadow: 0 0 10px #00a884;
  }
  
  /* Filter Buttons Styling */
  .map-filter-btn {
    background: #1e293b;
    color: #94a3b8;
    border: 1px solid #334155;
    padding: 5px 12px;
    font-size: 12px;
    border-radius: 15px;
    cursor: pointer;
    transition: all 0.2s ease;
  }
  .map-filter-btn:hover, .map-filter-btn.active {
    background: #00a884;
    color: #ffffff;
    border-color: #00a884;
    box-shadow: 0 0 8px rgba(0, 168, 132, 0.4);
  }

  /* Custom Cluster Styling */
  .marker-cluster-small, .marker-cluster-medium, .marker-cluster-large {
    background-color: rgba(0, 168, 132, 0.4) !important;
  }
  .marker-cluster div {
    background-color: #00a884 !important;
    color: #ffffff !important;
    font-weight: bold;
  }
</style>

<!-- Filter Controls -->
<div style="display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 10px;">
  <button class="map-filter-btn active" onclick="filterMap('all', this)">All Projects</button>
  <button class="map-filter-btn" onclick="filterMap('public-space', this)">Public Space</button>
  <button class="map-filter-btn" onclick="filterMap('resilience', this)">Recovery & Resilience</button>
  <button class="map-filter-btn" onclick="filterMap('tod', this)">Transport & TOD</button>
  <button class="map-filter-btn" onclick="filterMap('env', this)">Water & Climate</button>
  <button class="map-filter-btn" onclick="filterMap('research', this)">Academic & Field Research</button>
</div>

<!-- Map Container -->
<div id="experience-map" style="width: 100%; height: 400px; border-radius: 8px; margin-bottom: 2.5rem; background: #0f172a; border: 1px solid #1e293b;"></div>

<script>
  var map, markersCluster, allLocations = [];

  document.addEventListener("DOMContentLoaded", function() {
    map = L.map('experience-map', {
      center: [20.0, 15.0],
      zoom: 2,
      scrollWheelZoom: false
    });

    L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Dark_Gray_Base/MapServer/tile/{z}/{y}/{x}', {
      attribution: 'Tiles &copy; Esri',
      maxZoom: 16
    }).addTo(map);

    markersCluster = L.markerClusterGroup({
      maxClusterRadius: 35,
      spiderfyOnMaxZoom: true,
      showCoverageOnHover: false
    });

    allLocations = [
      // Jordan
      { name: "Ghor Safi, Jordan", focus: "Sports for Development Strategic Planning", cat: "public-space", coords: [31.0381, 35.4851] },
      { name: "Al-Salt, Jordan", focus: "Site-Specific Assessment for Public Space Design", cat: "public-space", coords: [32.0392, 35.7272] },
      { name: "Sahab, Jordan", focus: "City-Wide Assessment for Public Space Action Plan", cat: "public-space", coords: [31.8711, 36.0042] },
      { name: "Amman, Jordan", focus: "Strategic Urban Planning & Migration Context", cat: "resilience", coords: [31.9522, 35.2332] },
      { name: "Irbid, Jordan", focus: "Strategic Urban Planning & Migration Context", cat: "resilience", coords: [32.5568, 35.8469] },

      // Eastern Europe & Central Asia
      { name: "Kyiv, Ukraine", focus: "Urban Recovery Profile & Strategic Response Planning", cat: "resilience", coords: [50.4501, 30.5234] },
      { name: "Naryn, Kyrgyzstan", focus: "Urban Resilience Profile & Strategic Response Planning", cat: "resilience", coords: [41.4287, 75.9911] },
      { name: "Khorog, Tajikistan", focus: "Urban Resilience Profile & Strategic Response Planning", cat: "resilience", coords: [37.4916, 71.5530] },

      // Southeast Asia
      { name: "Semarang, Indonesia", focus: "Spatial Capital Investment Planning", cat: "resilience", coords: [-6.9667, 110.4167] },

      // Latin America & Caribbean
      { name: "Montevideo, Uruguay", focus: "Public Space City-Wide Assessment", cat: "public-space", coords: [-34.9011, -56.1645] },
      { name: "Santo Domingo, Dominican Republic", focus: "Public Space City-Wide Assessment", cat: "public-space", coords: [18.4861, -69.9312] },
      { name: "Monteria, Colombia", focus: "Public Space City-Wide Assessment", cat: "public-space", coords: [8.7479, -75.8814] },
      { name: "Lima, Peru", focus: "Environmental Management & Sensitization", cat: "env", coords: [-12.0464, -77.0428] },
      { name: "Santa Eulalia Sub-basin, Peru", focus: "Integrated Water Resources Management (IWRM) & Climate Adaptation", cat: "env", coords: [-11.8286, -76.6022] },

      // Saudi Arabia (TOD)
      { name: "Makkah, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [21.3891, 39.8579] },
      { name: "Dammam, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [26.4207, 50.0888] },
      { name: "Taif, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [21.2854, 40.4244] },
      { name: "Madinah, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [24.5247, 39.5692] },
      { name: "Qatif, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [26.5196, 50.0114] },
      { name: "Al Ahsa, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [25.3835, 49.5862] },
      { name: "Abha, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [18.2164, 42.5053] },
      { name: "Arar, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [30.9753, 41.0381] },
      { name: "Buraidah, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [26.3592, 43.9818] },
      { name: "Sakaka, Saudi Arabia", focus: "Sustainable Urban Development & Transport Oriented Planning", cat: "tod", coords: [29.9697, 40.2064] },

      // Academic & Field Research
      { 
        name: "Belén (Maynas, Loreto), Peru", 
        focus: "Undergraduate Thesis: Environmental Perception & Child Geography in Flooded Contexts", 
        cat: "research", 
        coords: [-3.7703, -73.2538] 
      },
      { 
        name: "Huaycán (Lima), Peru", 
        focus: "MSc Dissertation (LSE): Qualitative Governance & Community Leadership in Informal Settlements", 
        cat: "research", 
        coords: [-12.0160, -76.8220] 
      },
      { 
        name: "El Ayllu (Callao), Peru", 
        focus: "PUCP Applied Research: Involuntary Resettlement & Airport Infrastructure Impact", 
        cat: "research", 
        coords: [-12.0225, -77.1082] 
      }

          ];

    renderMarkers('all');
  });

  function renderMarkers(category) {
    markersCluster.clearLayers();

    var customIcon = L.divIcon({
      className: 'custom-map-marker',
      iconSize: [12, 12],
      iconAnchor: [6, 6]
    });

    allLocations.forEach(function(loc) {
      if (category === 'all' || loc.cat === category) {
        var marker = L.marker(loc.coords, { icon: customIcon })
          .bindPopup(`<strong style="color: #0f172a; font-size: 14px;">${loc.name}</strong><br/><span style="color: #334155; font-size: 12px; display: inline-block; margin-top: 4px;">${loc.focus}</span>`);
        markersCluster.addLayer(marker);
      }
    });

    map.addLayer(markersCluster);
  }

  function filterMap(category, btnElement) {
    document.querySelectorAll('.map-filter-btn').forEach(b => b.classList.remove('active'));
    btnElement.classList.add('active');
    renderMarkers(category);
  }
</script>

## Work Experience

<div class="timeline" markdown>

<div class="timeline-entry" markdown>

### Spatial Data Lead — UN-Habitat Jordan
*July 2025 – August 2026 | Amman, Jordan*

- Formulated spatial indicator frameworks, automated Remote Sensing workflows, and co-authored technical content for Public Space Diagnostics and Municipal Action Plans.
- Designed end-to-end spatial data architectures (from KoboToolbox mobile collection to executive Power BI dashboards) to embed evidence into local policy guidelines.
- Engineered a SQL-driven automated scoring framework to weight socio-environmental variables, establishing transparent site selection criteria for municipal asset maintenance.

</div>

<div class="timeline-entry" markdown>

### Spatial Data Management Specialist — UN-Habitat Ukraine Urban Lab
*February 2024 – June 2025 | Kyiv, Ukraine*

- Served as the strategic bridge between engineering labs (UNITAC/City Science Lab) and urban planners, translating "Build Back Better" modeling into actionable recovery policies.
- Managed spatial data operations across crisis-affected regions, integrating over 20 spatial layers across 8 municipalities into a unified Geodatabase Architecture.
- Systematized spatial diagnostic methodologies and QA protocols to establish a replicable framework for scalable urban recovery efforts.

</div>

<div class="timeline-entry" markdown>

### Spatial Data Analyst — UN-Habitat HQ & Global Public Space Programme
*January 2018 – December 2023 | Nairobi, Kenya*

- Operationalized high-level global agendas (SDGs, New Urban Agenda) into spatial proxy models and measurable indicators for data-scarce environments.
- Co-developed strategic mapping products, policy briefs, and concept notes to inform and technically assist local governments in evidence-based decision-making.
- Engineered network accessibility models, hazard risk matrices, and spatial database architectures (PostGIS/ETL) to inform urban mobility and climate-resilient planning.

</div>

<div class="timeline-entry" markdown>

### Programme Assistant — PUCP (DARS) & Global Water Partnership
*April 2014 – July 2016 | Lima, Peru*

- Performed satellite imagery processing and thematic mapping for regional water governance and river basin management in South America.
- Facilitated multi-level stakeholder coordination and led field teams for primary spatial data collection and technical validation.

</div>

</div>

---

## Education

### MSc in Regional and Urban Planning Studies
**London School of Economics and Political Science (LSE)** | *2017*

Focus on spatial economics, urban governance, and regional development policy.

---

### BA in Geography and Environment
**Pontifical Catholic University of Peru (PUCP)** | *2013*

Focus on GIS, spatial analysis, territorial planning, and environmental management.

---

## Certifications & Executive Education

- Specialization in PostGIS & SQL for GIS — Geoinnova (Spain), 2025
- Executive Program in Data Analytics — Datahack School (Spain), 2023
- Specialization in Territorial Management — INTE PUCP (Peru), 2015
- Specialization in Territorial Planning — INTE PUCP (Peru), 2015
