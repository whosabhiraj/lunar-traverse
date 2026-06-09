# 🌑 lunar-traverse

> Safe rover path planning for the lunar south pole — using real NASA LRO data to build a terrain hazard map and find the safest route for a rover.

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Data: NASA PDS](https://img.shields.io/badge/data-NASA%20PDS-red.svg)](https://pds.nasa.gov/)
[![Hack Club Stardance](https://img.shields.io/badge/Hack%20Club-Stardance-ec3750.svg)](https://stardance.hackclub.com/)

NASA's [Artemis program](https://www.nasa.gov/artemis) is sending astronauts back to the Moon, targeting the south pole — a region of extreme terrain, permanent shadow, and confirmed water ice. Planning a safe rover traverse there is a real engineering challenge: craters everywhere, slopes that would strand a vehicle, and areas with zero sunlight.

This project will build a path-planning pipeline using **real mission data** from NASA's Lunar Reconnaissance Orbiter. Starting from raw elevation data, it will:

1. **Process terrain data** — reproject and analyze NASA's LOLA digital elevation model
2. **Map hazards** — compute slope steepness, surface roughness, and detect craters
3. **Classify terrain with ML** — train a CNN on lunar imagery to identify hazardous terrain types
4. **Find the safest path** — use A* pathfinding on a combined hazard cost map
5. **Serve it as an API** — FastAPI endpoint where you input two coordinates and get the optimal path

> **Status:** Project just started. Currently setting up the development environment and data pipeline.

---

## Planned Pipeline

```
LOLA DEM ──▶ Reproject to Polar Stereographic ──▶ Slope Map + Roughness Map
                                                          │
LROC NAC ──▶ Crater Detection (Hough Transform) ─────────┤
         ──▶ CNN Terrain Classifier (ResNet-18) ──────────┤
                                                          ▼
                                               Traversability Cost Map
                                                          │
                                                          ▼
                                                    A* Path Planner
                                                          │
                                                          ▼
                                         Visualization + FastAPI Endpoint
```

---

## Data Sources

| Dataset | Instrument | Resolution | Purpose |
|---------|-----------|------------|---------|
| LOLA DEM | LRO / LOLA | ~5 m/px (south pole) | Primary elevation model |
| LROC NAC | LRO / LROC | 0.5 m/px | Crater detection + CNN training imagery |

All data is freely available from [NASA PDS](https://pds.nasa.gov/).

---

## Tech Stack

- **Python 3.11** with `uv` for dependency management
- **rasterio** + **pyproj** for geospatial data processing
- **OpenCV** for classical computer vision (crater detection)
- **PyTorch** for CNN terrain classification
- **Plotly** for interactive 3D visualization
- **FastAPI** for the REST API
- **numpy**, **scipy**, **matplotlib** for numerical work and plotting

---

## Project Context

Built for [Hack Club Stardance](https://stardance.hackclub.com/) — a NASA-partnered summer program. This project uses real mission data from NASA's Lunar Reconnaissance Orbiter, motivated by the genuine engineering challenge of surface operations at the lunar south pole for the Artemis program.

---

## License

MIT — see [LICENSE](LICENSE).
