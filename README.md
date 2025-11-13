# Water Mixing CFD Simulation - Architecture

## Overview

This project simulates hot and cold water mixing in a mug using computational fluid dynamics to analyze optimal pouring strategies.

---

## System Architecture

```
┌─────────────────────────────────────┐
│         Blender Interface           │
│      (Visualization & Control)      │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│      Blender Python Scripts         │
│    • Scene management               │
│    • Animation control              │
│    • Particle rendering             │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│       Python Bindings               │
│         (pybind11)                  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│    C++ Integration Layer            │
│    • Thermal dynamics               │
│    • Simulation coordinator         │
│    • Inflow management              │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│    SPH Fluid Library                │
│    (SPlisHSPlasH)                   │
│    • Particle physics               │
│    • Force computation              │
└─────────────────────────────────────┘
```

---

## Components

### SPH Fluid Library
- **Library**: SPlisHSPlasH
- **Purpose**: Core fluid dynamics simulation
- **Functionality**: Particle management, pressure/viscosity forces, collision handling

### C++ Integration Layer
- **Thermal Dynamics**: Heat diffusion and temperature tracking between particles
- **Buoyancy Module**: Temperature-dependent forces (hot water rises, cold sinks)
- **Simulation Coordinator**: Orchestrates fluid physics and thermal dynamics

### Python Bindings
- **Technology**: pybind11
- **Purpose**: Exposes C++ simulation to Python environment

### Blender Visualization
- **Scene Setup**: 3D mug geometry, camera, lighting
- **Animation**: Updates particle positions and colors per frame
- **Rendering**: Temperature-based color mapping, final video export

---

## Data Flow

```
1. Simulation initialization
   ↓
2. Blender calls C++ simulation step
   ↓
3. C++ integration layer:
   - Updates fluid physics (via SPH library)
   - Computes heat diffusion
   - Applies buoyancy forces
   ↓
4. Returns particle data (positions, temperatures)
   ↓
5. Blender updates visualization
   ↓
6. Repeat for each frame
```

---

## Project Structure

```
WaterMixing/
├── external/
│   └── SPlisHSPlasH/          # SPH library (git submodule)
│
├── cpp/
│   ├── include/
│   │   ├── thermal_dynamics.h
│   │   └── simulator.h
│   ├── src/
│   │   ├── thermal_dynamics.cpp
│   │   └── simulator.cpp
│   └── bindings/
│       └── python_bindings.cpp
│
├── blender/
│   ├── setup_scene.py
│   ├── run_simulation.py
│   └── visualize.py
│
├── build/
│   └── water_mixing.so        # Compiled module
│
└── results/
    ├── videos/
    └── data/
```

---

## Technology Stack

- **C++17**: Core simulation code
- **SPlisHSPlasH**: SPH fluid dynamics library
- **pybind11**: C++/Python interoperability
- **Blender 3.x**: 3D visualization and rendering
- **Python 3.10+**: Scripting and automation
- **CMake**: Build system

---

## Key Features

- Real-time CFD simulation with SPH method
- Custom thermal dynamics implementation
- Temperature-driven buoyancy effects
- Interactive Blender visualization
- Comparative analysis (cold-first vs hot-first pouring)

---
