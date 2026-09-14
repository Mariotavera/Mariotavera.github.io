<!--
CHECKLIST FOR THIS PAGE (copy this file for each new project):
- [ ] Replace [YOUR PROJECT TITLE] with your project title
- [ ] Replace the hero image with your own (add to docs/assets/images/)
- [ ] Update the Overview section
- [ ] Update the Methods & Tools section
- [ ] Update the Key Findings section
- [ ] Update the Links section
- [ ] Add a card for this project on docs/projects/index.md
- [ ] Add a nav entry in mkdocs.yml
-->

![](../assets/images/project3-svg.svg){ style="width:100%; max-height:250px; object-fit:cover; border-radius:8px;" }

# Localized Spatial Analytics Engine for SDG 11.7.1 Monitoring

**Target** Department of Statistics and Local Authorities | **Period:** 2026 | **Role:** Lead Geospatial Data Specialist & Developer (Solo Project) | **Status:** Under Mantainance

---

## Overview & Institutional Context

Monitoring universal access to safe, inclusive, and accessible green and public spaces (SDG Indicator 11.7.1) presents a critical challenge for national statistical offices and local authorities in developing contexts. Traditional GIS workflows rely on static buffer analyses or centralized cloud solutions, which frequently fail to account for complex pedestrian network topologies and compromise sensitive demographic microdata.

To address this, its required a localized, high-precision analytical pipeline capable of processing high-resolution demographic microdata while strictly preserving national data sovereignty. As the **Lead Geospatial Data Specialist & Developer**, I engineered a decentralized, containerized Web GIS application. The engine automates end-to-end spatial access modeling by integrating Uber H3 spatial indexing, dynamic pedestrian network routing, and custom topological bias correction within a zero-dependency, locally executable architecture.

---

## Methodology & Data Architecture

#### Data Sources & Field Collection

* **National Statistics Office or Local Authority:** Confidential high-resolution demographic microdata, administrative spatial boundaries, and validated municipal open public space inventories.
* **Open Spatial Network Data (OSMnx API):** High-precision pedestrian road networks and path topologies extracted and densified dynamically for the target study areas.

#### System Architecture & Pipeline

The system utilizes a decoupled Web GIS architecture where a Streamlit frontend acts as a dynamic orchestration layer, triggering modular Python analytics pipelines (`pipeline_core.py`) completely in-memory to eliminate external cloud exposures and guarantee local data governance.

=== "1. End-to-End Architecture (Overview)"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project3-architecture.png" 
           alt="End-to-End SDG 11.7.1 System Architecture" 
           style="max-height: 420px; width: auto; object-fit: contain; border-radius: 6px;">
    </div>

    **High-Level System Integration**

    * **In-Memory Data Ingestion:** Automated parsing, schema-agnostic validation, and attribute identification of spatial layers without persistent local disk staging.
    * **Graph & Grid Engine:** Disaggregation of demographic microdata into Uber H3 discrete global grids paired with OSMnx graph retrieval and densification.
    * **Parametric Simulation & UI:** Real-time execution of topological network routing, matrix reconciliation, and dynamic spatial staging in Folium.


=== "2. Frontend Interfaces & Scenario Controls (`app.py`)"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project3-front.png" 
           alt="Processing Pipeline and Topological Reconciliation" 
           style="max-height: 420px; width: auto; object-fit: contain; border-radius: 6px;">
    </div>

    **Processing Steps:**

    * **Sidebar & Ingestion Setup:** Dynamic upload stage handling study boundaries, demographic points, and destination vectors. Automated WGS84 CRS validation (`ensure_wgs84`), Streamlit `session_state` persistence, and schema configuration for ID and population attributes.
    * **Input Audit Panel:** Instant spatial sanity checks powering interactive PyDeck territorial previews, population distribution summaries, and destination inventory counts prior to pipeline execution.
    * **Parameters & Execution Mode:** User-defined configuration for walking speeds (km/h) and time thresholds (minutes), triggering either single-zone localized diagnostics or multi-zone batch execution modes.
    * **Pipeline Core Invocation:** Execution of `compute_zone_accessibility()` via in-memory data streams, passing validated GeoDataFrames directly to the analytical engine without disk writing.
    * **Reporting & Export Center:** Staging of spatial outputs featuring dynamic SDG indicator KPIs, interactive Folium accessibility maps (Green: Covered / Red: Deficit), and on-demand spatial exports (`CSV` / `GeoJSON`).

=== "3. Backend Pipeline & Network Reconciliation (`pipeline_core.py`)"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project3-back.png" 
           alt="Processing Pipeline and Topological Reconciliation" 
           style="max-height: 420px; width: auto; object-fit: contain; border-radius: 6px;">
    </div>

    **Processing Steps:**

    * **Pre-Processing & Spatial Extraction:** Automatic buffer computation (`get_buffer_dist`) to fetch street graphs via OSMnx (`acquire_pedestrian_network & densify_and_export`) and disaggregate population points into H3 hexagonal grids (`generate_h3_origins`).
    * **Tabular Bias Check:** Simultaneous generation of network node-snapping tables (`generate_snap_tables`) and direct origin-to-destination distance matrices (`build_euclidean_distance_matrix`) to detect routing anomalies (`flag_snap_bias`).
    * **Routing & Matrix Optimization:** NetworkX shortest-path computation (`calculate_accessibility_matrix`) coupled with custom hierarchical bias correction (`apply_hierarchical_bias_correction`) to resolve node-snapping detours when nearest nodes exceed Euclidean destination distance.
    * **Temporal Thresholding & Export Staging:** Extraction of optimal spatial access paths (`extract_best_accessibility`), integration of spatial metrics, and application of dynamic temporal cuts (`apply_temporal_thresholding`) to feed formatted GeoDataFrames back to the frontend exporter.


### Output Delivered

The analytical engine culminates in a **containerized, interactive Web GIS platform** that transforms static spatial indicators into a dynamic decision-support system. Operating entirely in-memory within an isolated Docker/WSL2 environment, the application enables statistical officers to execute scenario-based accessibility simulations, adjust walking speeds and temporal thresholds on the fly, and visualize real-time demographic coverage without exposing confidential microdata to third-party cloud services.

=== "1. Welcome Interface"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project3-interface.png" 
           alt="SDG 11.7.1 Welcome Interface and Ingestion Setup" 
           style="width: 100%; max-width: 900px; height: 400px; object-fit: contain; border-radius: 8px; border: 1px solid #e2e8f0; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);">
      <p style="font-size: 0.85em; color: #64748b; margin-top: 0.8em; font-style: italic;">
        <strong>Figure 1:</strong> System Landing & Drag-and-Drop Ingestion Panel — Interactive sidebar for loading GeoJSON spatial layers (boundaries, population, destinations) and setting real-time simulation parameters (walking speeds and time thresholds).
      </p>
    </div>

=== "2. Input Data Audit"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project3-interface2.png" 
           alt="Input Data Validation & Ingestion Panel" 
           style="width: 100%; max-width: 900px; height: 400px; object-fit: cover; object-position: center 30%; border-radius: 8px; border: 1px solid #e2e8f0; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);">
      <p style="font-size: 0.85em; color: #64748b; margin-top: 0.8em; font-style: italic;">
        <strong>Figure 2:</strong> Spatial Sanity & Attribute Audit — Automated spatial boundary parsing and interactive PyDeck preview for dynamic category filtering and territorial attribute configuration prior to graph routing execution.
      </p>
    </div>

=== "3. SDG Calculation & Spatial Mapping"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project3-interface3.png" 
           alt="Accessibility Indicators Report and Spatial Mapping" 
           style="width: 100%; max-width: 900px; height: 400px; object-fit: cover; object-position: center 20%; border-radius: 8px; border: 1px solid #e2e8f0; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);">
      <p style="font-size: 0.85em; color: #64748b; margin-top: 0.8em; font-style: italic;">
        <strong>Figure 3:</strong> Automated Analytics & Isochrone Visualizer — Real-time consolidation of SDG population coverage metrics, paired with interactive Folium maps highlighting covered H3 cells versus underserved deficit areas.
      </p>
    </div>

=== "4. Download Datasets & Report"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project3-interface4.png" 
           alt="Download Datasets and Executive Report Panel" 
           style="width: 100%; max-width: 900px; height: 400px; object-fit: contain; border-radius: 8px; border: 1px solid #e2e8f0; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);">
      <p style="font-size: 0.85em; color: #64748b; margin-top: 0.8em; font-style: italic;">
        <strong>Figure 4:</strong> Export Center & Reporting Staging — On-demand generation and export of consolidated CSV indicator summaries, spatial GeoJSON H3 grid layers, and cleaned destination feature sets for institutional archiving.
      </p>
    </div>


**Tools Used**

| Tool | Purpose |
|------|---------|
| **Python (GeoPandas, SciPy, NetworkX)** | Vector data manipulation, topological network analysis, and Euclidean/network matrix reconciliation. |
| **OSMnx & Uber H3** | Automated pedestrian graph retrieval and discrete global grid system indexing for population aggregation. |
| **Streamlit & PyDeck / Folium** | Interactive Web GIS frontend interface, parametric controls, and dynamic spatial visualization. |
| **Docker & WSL2** | Isolated, zero-dependency containerized execution environment guaranteeing local data governance. |

---
<div style="margin-top: 2em; text-align: center;">
  <a href="../" class="md-button md-button--primary" style="margin-right: 10px;">← Back to Projects</a>
</div>


---

## Links

[View Code on GitHub](https://github.com/[YOUR-GITHUB-USERNAME]/[YOUR-REPO-NAME]){ .md-button }
[View Data Source](https://example.com){ .md-button }
