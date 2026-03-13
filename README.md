<div align="center">

# PiezoSolar NanoGrid

### A Hybrid Human–Solar Energy Harvesting and AI-Optimized DC Nano-Grid for Climate-Resilient Communities

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: Active Development](https://img.shields.io/badge/Status-Active%20Development-brightgreen.svg)]()
[![SDG 7](https://img.shields.io/badge/SDG-7%20Clean%20Energy-orange.svg)]()
[![SDG 13](https://img.shields.io/badge/SDG-13%20Climate%20Action-green.svg)]()
[![Made in Bangladesh](https://img.shields.io/badge/Made%20in-Bangladesh-red.svg)]()

*Turn every footstep and every sunbeam into measurable, optimizable, and community-serving electricity.*

</div>

---

## Overview

**PiezoSolar NanoGrid** is a modular, community-scale clean energy platform designed for **climate-vulnerable, grid-unreliable, and high-footfall communities**. It combines two complementary renewable sources, **piezoelectric floor tiles** that harvest energy from footsteps and **solar PV panels** that capture sunlight, and distributes power through an intelligent **48V DC nano-grid** optimized in real time by AI/ML forecasting, IoT monitoring, Particle Swarm Optimization (PSO), and a blockchain-verified carbon accounting layer.

The system is purpose-built for settings such as **market corridors, university campuses, railway approaches, informal business zones, and disaster-prone community spaces**, where human movement and sunlight are abundant, but reliable electricity is not.

---

## Problem Statement

Over **666 million people** worldwide still lack basic electricity access. Bangladesh, despite producing only **0.3% of global greenhouse gas emissions**, ranks as the **9th most climate-vulnerable nation** on the 2024 World Risk Index. Key challenges include:

- Chronic load-shedding with shortfalls regularly exceeding **1,500–2,000 MW daily**
- Rural micro-enterprises enduring **9–12 hours of daily outages**
- Heavy fossil-fuel dependence (**65% of total power supply**)
- Solar nano-grids are limited by intermittency and lack intelligent load management
- Zero integration of existing decentralized systems with carbon markets
- Vast amounts of kinetic energy in densely populated pedestrian spaces are going entirely unharvested

No existing system combines solar PV generation, piezoelectric kinetic harvesting, AI optimization, and carbon market integration into a single, affordable, community-scale solution. PiezoSolar NanoGrid addresses that gap.

---

## Solution

PiezoSolar NanoGrid treats **solar energy and human kinetic energy as complementary sources**, coordinated through a data-driven DC architecture built for micro-enterprises, local resilience, and long-term scale.

### Comparison with Existing Approaches

| Feature | Solar-Only Nano-Grid | Piezo Floor Alone | PiezoSolar NanoGrid |
|---|---|---|---|
| Night / cloudy-day generation | No | Limited (traffic-dependent) | Yes |
| Daytime generation | Yes | Minimal | Yes |
| AI load optimization | No | No | Yes |
| Real-time IoT monitoring | No | No | Yes |
| Carbon credit integration | No | No | Yes |
| Crowd analytics (secondary output) | No | No | Yes |

---

## Six-Layer Innovation Stack

### Layer 1 — Piezoelectric Energy Harvesting

Modular floor tiles (300 x 300 mm) embed **PZT/PVDF composite transducers** in a bidirectional mechanism that captures energy on both the compression and release phases of each footstep, effectively doubling per-step energy capture compared to unidirectional designs.

- Each tile: 6–8 PZT-5A discs in series, generating approximately 12–16V per footstep under a 50–75 kg load
- Arrays of 50–200 tiles deployed across high-traffic corridors
- IP65-rated, flood-resistant polycarbonate housing; no structural modification to existing surfaces required

### Layer 2 — Solar-DC Nano-Grid

Thin-film solar PV panels (amorphous silicon or CIGS) feed a **DC-optimized nano-grid** built around a 48V bus, avoiding the 15–20% conversion losses of traditional AC systems.

- MPPT charge control per panel pair
- Star/radial topology distributing power to load points within 200–500 m
- Builds on validated Solar-DC nano-grid architecture from prior prototype work (SolarSpark Bangladesh)

### Layer 3 — AI/ML Energy Optimization

Forecasting models predict generation and drive proactive scheduling:

- **Footfall Prediction DNN** (3-layer, 128–64–32 neurons, ReLU, dropout 0.2): predicts hourly piezoelectric generation from pedestrian count history, time-of-day features, and weather context
- **Solar Irradiance Forecaster** (XGBoost): predicts hourly PV output from cloud cover, rain probability, and temperature
- **Integrated 24-hour generation forecast**: enables proactive battery pre-charging and load scheduling ahead of peak demand
- Target accuracy: R² > 0.85 on held-out test sets

### Layer 4 — IoT Monitoring and Control

Self-powered sensor nodes stream real-time operational data to a centralized dashboard every 5 seconds via BLE.

| Sensor | Parameter Measured | Sampling Rate |
|---|---|---|
| INA219 | Piezo / Solar voltage and current | 1–10 Hz |
| MPU6050 | Footfall count and step force | 50 Hz |
| DHT22 | Temperature and humidity | 0.1 Hz |
| BQ34Z100 | Battery State of Charge | 1 Hz |

Data pipeline: ESP32 edge processing → BLE → Raspberry Pi gateway → Cloud DB (InfluxDB / Firebase) → AI inference engine → Power BI / Streamlit dashboard → control commands to PMU.

### Layer 5 — Swarm Intelligence Coordination

A **Particle Swarm Optimization (PSO)** controller re-optimizes every 15 minutes across three decision variables:

- Battery charge/discharge rate
- Load priority allocation (lighting > charging > appliances)
- Carbon credit maximization through surplus energy routing

The objective function minimizes total unmet load cost and battery degradation cost while maximizing carbon credit revenue, subject to bus voltage constraints (42V–54V) and battery SoC limits (20%–95%). The Python-based implementation completes each optimization cycle in under 2 seconds on the Raspberry Pi gateway.

### Layer 6 — Blockchain Carbon Credit System

Every verified renewable kWh is converted into a traceable climate value through a five-step chain:

1. IoT logs each kWh with timestamp, source ID, and cryptographic hash (SHA-256)
2. CO2 avoided = kWh × 0.60 kg CO2/kWh (Bangladesh Combined Margin grid emission factor)
3. Data written to Hyperledger Fabric (or Ethereum testnet) as immutable, tamper-proof records
4. Smart contract automatically mints a carbon micro-credit token when cumulative offsets reach 1 ton CO2
5. Credits are tradeable on voluntary carbon markets (current prices: $4–15/ton CO2)

---

## System Architecture

```
Footsteps + Sunlight
        |
        |-- Piezo Tile Array -- Rectification / Boost --+
        |-- Solar PV + MPPT -----------------------------|
        |                                               |
        +---------------> 48V DC Bus / PMU <------------+
                               |
                +--------------+---------------+
                |              |               |
           LiFePO4 Pack  Supercapacitors   Smart Loads
           (960 Wh)      (pulse buffer)   (metered branches)
                |                              |
                +------- IoT Telemetry --------+
                               |
                     Gateway / Data Pipeline
                               |
                 AI Forecasting + PSO Optimization
                               |
              Power BI Dashboard + Carbon Blockchain Log
```

---

## Technical Specifications

### Hardware

| Component | Specification |
|---|---|
| Piezo tile dimensions | 300 x 300 x 25 mm |
| Transducers | PZT-5A discs (27 mm dia, 0.5 mm thick) + PVDF film |
| Tile output | ~12–16V peak per footstep |
| Solar panels | Flexible thin-film, 50W per panel |
| DC bus voltage | 48V nominal |
| Battery | LiFePO4, 48V, 20 Ah (960 Wh), sealed |
| Pulse buffer | Supercapacitor bank (100F, 48V) |
| Distribution wiring | 2.5 mm² copper, UV-resistant conduit, 200–500 m radial |
| Bus protection | UVLO at 42V, OVP at 54V, e-fuse per branch, surge MOV |

### Embedded and IoT Stack

- Microcontroller: ESP32 (BLE + Wi-Fi)
- Sensors: INA219, MPU6050, DHT22, BQ34Z100
- Gateway: Raspberry Pi with MQTT broker and InfluxDB
- Connectivity: BLE to Wi-Fi / 4G to cloud

### Software Stack

| Layer | Technology |
|---|---|
| AI forecasting | Python, XGBoost, Keras / PyTorch DNN |
| Optimization | Python, NumPy-based PSO |
| Dashboard | Power BI (primary), Streamlit (real-time backup) |
| Blockchain | Hyperledger Fabric / Ethereum testnet |
| Simulation | COMSOL Multiphysics, MATLAB/Simulink |
| Data pipeline | InfluxDB, Firebase, MQTT |

---

## Expected Impact

### Energy Generation Targets

| Configuration | Projected Daily Output | Load Served |
|---|---|---|
| Pilot: 50 tiles + 4 x 50W solar panels | 1.3–3.0 kWh/day | 3–5 micro-enterprise units |
| Scale: 200 tiles + 1 kW PV array | 5–10 kWh/day | 10–15 vendors with evening hours |

### Broader Outcomes

- 60–70% energy cost reduction for served micro-enterprises
- 1.5–2.2 tons CO2 avoided per year per pilot site
- $10–30/year additional revenue from carbon micro-credits per site
- Off-grid resilience for cyclone shelters and flood evacuation corridors
- New local green jobs in installation, monitoring, and maintenance
- Replicable architecture for South Asia, Sub-Saharan Africa, and Pacific Island states

---

## Target Use Cases

**Community and commercial settings:**
- Market walkways and vendor corridors
- University campuses
- Railway platform approaches
- Informal business clusters and off-grid settlements

**Resilience and humanitarian settings:**
- Cyclone shelter corridors
- Flood-response and emergency lighting zones
- Community phone-charging points during outages
- Low-power communication support nodes

---

## Project Lineage

PiezoSolar NanoGrid converges two independently validated research and prototype tracks:

1. **Piezoelectric Energy Floor** — the concept lineage earned **Third Prize, South Asian Division**, at the *2nd ISETS-ESCAP & 3rd ISETS Global Competition of Youth Voice on Energy Transition (2025)*, submitted under **Roots of Rise**, a non-profit organization that works for the community to develop it and make it great.
2. **Solar-DC Nano-Grid (SolarSpark Bangladesh)** — advanced to **Phase 2 of the Global Sustainability Challenge**, with submissions reviewed ahead of the IIT Bombay regional stage.

PiezoSolar NanoGrid merges both streams into one integrated system, combining the kinetic-energy harvesting vision with the practical DC distribution architecture proven in the solar track.

---

## Repository Structure

```
PiezoSolar-NanoGrid/
├── README.md
├── docs/
│   ├── concept-note/
│   ├── literature-review/
│   ├── deployment-plan/
│   └── impact-model/
├── hardware/
│   ├── tile-design/
│   ├── power-electronics/
│   ├── battery-system/
│   └── schematics/
├── firmware/
│   ├── esp32-sensors/
│   ├── gateway/
│   └── communication/
├── software/
│   ├── forecasting/
│   ├── pso-controller/
│   ├── dashboard/
│   └── carbon-logging/
├── data/
│   ├── pilot/
│   ├── processed/
│   └── benchmarks/
├── simulations/
│   ├── comsol/
│   ├── matlab-simulink/
│   └── power-flow/
├── media/
│   ├── diagrams/
│   ├── photos/
│   └── assets/
└── LICENSE
```

---

## Development Roadmap

### Phase 1 — Research and Design
- [x] Concept formulation and literature review
- [ ] COMSOL Multiphysics simulation of piezo tile stress distribution and voltage output
- [ ] MATLAB/Simulink hybrid DC nano-grid power flow modeling
- [ ] PSO objective function and constraint specification
- [ ] Component selection and procurement

### Phase 2 — Prototype Build
- [ ] Fabricate 4 piezoelectric floor tiles
- [ ] Integrate 2 x 50W solar panels with MPPT controllers
- [ ] Assemble 48V LiFePO4 battery pack with Battery Management System
- [ ] Bench-test bus stability and combined output

### Phase 3 — Data and Intelligence
- [ ] Deploy ESP32 sensor nodes with BLE telemetry
- [ ] Establish Raspberry Pi gateway with InfluxDB and MQTT pipeline
- [ ] Train DNN footfall prediction model on simulation and public pedestrian datasets
- [ ] Implement PSO scheduling controller in Python
- [ ] Build a Power BI and Streamlit dashboard
- [ ] Deploy Hyperledger / Ethereum testnet smart contract prototype

### Phase 4 — Field Pilot
- [ ] Deploy in the university campus corridor or the market walkway in Dhaka
- [ ] Run 7–14 days of continuous operation
- [ ] Compare against solar-only baseline of equivalent capacity
- [ ] Collect and analyze generation, load, and reliability data

### Phase 5 — Scale and Replication
- [ ] Package design files for broader deployment
- [ ] Open-source hardware and software release
- [ ] Evaluate replication across South Asia and other climate-vulnerable regions
- [ ] Aggregate carbon credits toward registry-listed portfolios

---

## Research Questions

This project operates simultaneously as an engineering system and a research platform. Key open questions include:

1. How much useful low-voltage electricity can a hybrid piezo-solar system generate under real high-footfall conditions?
2. Does adding piezoelectric harvesting materially improve resilience or economics over solar-only nano-grids?
3. Can AI forecasting and PSO control improve battery utilization, load service rate, and overall system efficiency?
4. What deployment conditions make the system most viable for micro-enterprise electrification in developing-country contexts?
5. How should community-scale renewable microgeneration be measured, verified, and reported for climate-finance relevance?

---

## SDG Alignment

| Goal | Connection |
|---|---|
| **SDG 7** — Affordable and Clean Energy | Direct: clean electricity access for energy-poor communities |
| **SDG 9** — Industry, Innovation and Infrastructure | Direct: novel hybrid engineering system for underserved infrastructure contexts |
| **SDG 11** — Sustainable Cities and Communities | Direct: resilient urban micro-infrastructure in climate-stressed settlements |
| **SDG 13** — Climate Action | Direct: measurable CO2 avoidance with blockchain-verified carbon credit integration |

The project also aligns with **Dr. Muhammad Yunus's Three Zero Theory** (Zero Poverty, Zero Unemployment, Zero Net Carbon Emissions), which the Government of Bangladesh has incorporated into its national SDG implementation framework.

---

## Contributing

Contributions are welcome across all project layers:

- Hardware design (tiles, power electronics, battery systems)
- Embedded firmware (ESP32, Raspberry Pi gateway)
- AI/ML forecasting and PSO optimization
- Dashboard engineering (Power BI, Streamlit)
- Carbon accounting and blockchain smart contracts
- Field deployment design and community engagement
- Documentation and impact modeling

To contribute, open an issue describing your area of interest or submit a pull request. See `CONTRIBUTING.md` for detailed guidelines.

---

## Citation

If you use this project as inspiration, reference material, or part of academic or engineering work, please cite the repository:

```bibtex
@misc{chowdhury_piezosolar_nanogrid_2026,
  author       = {Md Emon Chowdhury},
  title        = {PiezoSolar NanoGrid: A Hybrid Human-Solar Energy Harvesting
                  and AI-Optimized DC Nano-Grid for Climate-Resilient Communities},
  year         = {2026},
  howpublished = {GitHub Repository},
  note         = {https://github.com/[EmonChowdhury72]/PiezoSolar-NanoGrid}
}
```

Key references informing this project include the Cairo Stadium PV-Piezo Hybrid Floor study, the Solar-DC Nano-Grid design for Bangladesh (Appropedia), PSO for microgrid energy management, the IEA/IRENA Tracking SDG 7 Report (2025), and UNCTAD Voluntary Carbon Markets (2025).

---

## License

- **Code:** [MIT License](LICENSE)
- **Documentation:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

---

## Contact

**Md Emon Chowdhury**  
Entrepreneur · Aspiring Economist · Researcher  
Co-founder & CEO, WasteWiz | Founder, Roots of Rise  
Dhaka, Bangladesh

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/-emon-chowdhury26688/)

---

<div align="center">

*PiezoSolar NanoGrid is built on a simple conviction: communities should not have to wait for perfect infrastructure before they get reliable, intelligent, and dignified energy systems. If the grid is inconsistent, the climate is hostile, and capital is scarce, the answer has to be better design.*

</div>
