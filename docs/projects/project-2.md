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

![](../assets/images/project2-svg.svg){ style="width:100%; max-height:250px; object-fit:cover; border-radius:8px;" }

# Automated Public Space Scoring for Action Plan Development

**Study Area:** Sahab Municipality, Jordan | **Duration:** 2026 | **Role:** Lead Spatial Data Engineer & Analyst | **Status:** Completed

---

## Overview & Institutional Context

In rapidly urbanizing contexts across the Middle East, municipal authorities face severe challenges in evaluating public space quality and prioritizing capital investments efficiently. Traditional urban assessment methods rely on manual field evaluations that often result in static reports and subjective decision-making.

To solve this, the **UN-Habitat Jordan Country Programme** initiated the **Sahab Public Space Strategy**, requiring a scalable spatial data pipeline capable of transforming high-density microdata into automated, site-specific municipal action plans.

As the **Lead Spatial Data Engineer & Analyst**, I architected and deployed an automated spatial database engine inside **PostgreSQL/PostGIS**. The system ingests raw field survey data, executes topological street tessellations, computes a multi-dimensional urban quality score (**Accessibility, Environment, Inclusivity**), and triggers automated benchmark-driven diagnoses to prioritize municipal interventions across short, medium, and long-term action plans.

---

## Methodology & Data Architecture

#### Data Sources & Field Collection

* **Municipal Cadastre & Land Administration:** High-resolution parcel boundaries provided by the municipality, serving as the topological foundation to identify public space units and drive the street vector polygonization process.
* **Open Spatial Data & Satellite Intelligence:** OpenStreetMap street networks, building vectors, and Earth Observation derivatives (e.g., Sentinel-2 NDVI spectral indices) for baseline environmental and spatial metrics.
* **KoboToolbox Field Microdata:** Structured mobile survey data capturing high-density physical conditions, safety features, vegetation diversity, and localized user perceptions directly linked to spatial units.

#### System Architecture & Pipeline

The pipeline operates on an **ETL architecture built entirely inside PostgreSQL/PostGIS**. The system is structured into two sequential stages: a **Diagnostic Phase**—focused on field data collection, multi-dimension spatial analysis, and automated baseline evaluation—and a **Strategic Planning Phase**, which synthesizes **synthetic diagnostic scores, planner-defined urban benchmarks, and macro-level spatial structures** to generate actionable urban plans for dynamic dashboard visualization.

=== "1. End-to-End Architecture (Overview)"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project2-architecture-macro.png" alt="Sahab Spatial Database Pipeline Overview" style="max-height: 540px; width: auto; object-fit: contain; border-radius: 6px;">
    </div>

    **High-Level System Integration**

    * **Data Ingestion & Field Collection:** Syncing KoboToolbox microdata and spatialized public space inventory units directly into PostgreSQL.
    * **Automated Baseline Analytics:** Multi-dimensional scoring and dynamic SQL-driven diagnostic evaluation.
    * **Action Plan & Dashboard Synthesis:** Parameterization of planning rules and dynamic view staging to feed the interactive dashboard.

=== "2. Phase 1: Baseline Diagnostic Pipeline"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project2-architecture-phase1.png" alt="Phase 1 Diagnostic Pipeline Schema" style="max-height: 540px; width: auto; object-fit: contain; border-radius: 6px;">
    </div>


    **Processing Steps:**

    * **Parallel Staging & Spatial Boundary Setup:** Simultaneous execution of spatial unit boundary creation (derived from municipal cadastral polygons and street centerlines) and field survey instrument design in KoboToolbox, which is strictly structured around the project's **core analytical framework** to ensure indicator alignment.
    * **Field Collection & Multi-Source ETL Ingestion:** High-density field data capture synced to PostgreSQL/PostGIS. Raw microdata undergoes automated cleaning, typographical correction, categorical grouping for open-ended responses, and schema mapping into normalized database tables.
    * **Rule-Based Analytics & Diagnostic Synthesis:** Execution of SQL-driven mathematical models using response values, operational parameters, custom behavior formulas, and weighted subdimension aggregations to generate quantifiable indicators and diagnostic maps.

=== "3. Phase 2: Strategic Planning & Action Plan"

    <div style="text-align: center; margin: 1.5em 0;">
      <img src="/assets/images/project2-architecture-phase2.png" alt="Phase 1 Diagnostic Pipeline Schema" style="max-height: 540px; width: auto; object-fit: contain; border-radius: 6px;">
    </div>

    **Processing Steps:**

    * **Analytical Temporal Phasing:** Automated categorization of intervention horizons (*Short, Medium, and Long-Term Action Plans*) driven directly by Phase 1 diagnostic scores, unit-level valuation, and deficiency severity metrics.
    * **Spatial Integration of Urban Structure & Governance:** Vectorization and spatial overlay of macro urban planning elements (strategic nodes, activity corridors) paired with local governance boundaries (**neighborhood administrative limits**).
    * **Automated Benchmark Diagnostic Joins:** Dynamic execution of relational queries using composite primary keys (pairing unique public space unit codes with unique variable identifiers) to automatically flag localized strengths and weaknesses.


#### Output Delivered

The spatial analytical engine culminates in an **interactive web dashboard powered by dynamic PostGIS database views**. By amalgamating baseline diagnostic scores, planner-defined benchmark flags, and macro urban structures into optimized SQL materialized views, the platform bridges back-end geospatial engineering with executive decision-making. 

<div style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/project2-dashboard.png" 
       alt="Sahab Interactive Public Space Dashboard" 
       style="width: 100%; max-width: 900px; border-radius: 8px; border: 1px solid #e2e8f0; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);">
  <p style="font-size: 0.85em; color: #64748b; margin-top: 0.8em; font-style: italic;">
    <strong>Figure:</strong> Executive Dashboard Interface — Integrating live spatial queries, spatialized rank sorting (Rank_st / Rank_dyn), and temporal phasing filters.
  </p>
</div>



---

## Tools Used

| Tool | Purpose |
| --- | --- |
| **PostgreSQL & PostGIS**| Core spatial database engine, Voronoi tessellation, spatial joins, and unpivoted view transformations. |
| **KoboToolbox**| Mobile spatial data collection and field survey management. |
| **SQL (pgSQL)**| Advanced query development including `LATERAL JOIN`, `ST_VoronoiPolygons`, and rule-based triggering. |
| **ArcGIS** | GIS vector editing, topological validation, and spatial layer preparation. |
| **Sahab Dashboard** | Interactive PowerBI for visualizing action plan clusters and diagnostic profiles. |

---

<div style="margin-top: 2em; text-align: center;">
  <a href="../" class="md-button md-button--primary" style="margin-right: 10px;">← Back to Projects</a>
</div>

---

## Links

[View Code on GitHub](https://github.com/[YOUR-GITHUB-USERNAME]/[YOUR-REPO-NAME]){ .md-button }
[View Data Source](https://example.com){ .md-button }
