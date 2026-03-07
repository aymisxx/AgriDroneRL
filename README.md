# **AgriDroneRL**

### NDVI-Based Drone Navigation using Reinforcement Learning  
**(PPO vs DQN vs A2C: A Comparative Study)**

**Author**: Ayushman M. (https://github.com/aymisxx)

---

## Project Overview

**AgriDroneRL** investigates vision-based autonomous drone navigation over agricultural fields using reinforcement learning. A fixed-altitude drone observes a local 128×128 vegetation patch extracted from a satellite-derived NDVI proxy and selects discrete motion actions to maximize informative field coverage.

## Problem Statement

Efficient monitoring of large agricultural fields is critical for early detection of plant health issues, stress patterns, and spatial variability in crop conditions. Manual inspection or dense sensor deployment is often impractical due to scale and cost. In this project, the objective is to autonomously maximize the coverage of vegetation-rich regions within an agricultural field using a vision-guided drone agent. The environment provides a proxy vegetation signal (NDVI-inspired metric) derived from aerial imagery, allowing the agent to identify and prioritize areas with meaningful plant presence. The task is formulated as a reinforcement learning problem where the drone must navigate the field efficiently, discover vegetation zones, and maximize cumulative green coverage while minimizing redundant exploration. This framework explores how learning-based navigation policies can enable autonomous agricultural monitoring systems that prioritize biologically relevant regions rather than performing naive uniform coverage.

---

## Environment Design

- **Vegetation Map:** VARI-based NDVI proxy computed from RGB satellite imagery, normalized to [0, 1].  
- **Observation:** 128×128 local vegetation window, single-channel image `(1, 128, 128)`.  
- **Action Space:** Discrete(4) - up, right, down, left (boundary-clamped).  
- **Reward:** NDVI value on first visit to a cell, zero on revisits.  
- **Episodes:** Fixed-length, SB3-compatible.

### **Simulation Environment**

The custom made simulation environment used:
> https://github.com/aymisxx/MicroUAV-2D

---

## Algorithms Compared

- PPO (Proximal Policy Optimization).  
- DQN (Deep Q-Network).  
- A2C (Advantage Actor-Critic).  

All algorithms share the same environment, episode length, and evaluation pipeline.

---

## Evaluation Metrics

- Episode return.  
- Unique visited cells.  
- Coverage ratio.  
- Mean and median NDVI of visited cells.  

Trajectory GIFs are generated for qualitative comparison.

---

## Folder Structure

```
AgriDroneRL
├── data/
│   ├── field_satellite.jpg
│   └── ndvi_field.npy
├── models/
│   └── ppo_ndvi_drone.zip
├── results/
│   (trajectory plots)
├── AgriDroneRL_Main_PPO.ipynb
├── AgriDroneRL_Comparative.ipynb
├── requirements.txt
└── README.md
```

## How to Run

1. Place a satellite image in `data/field_satellite.jpg`.

2. Open the Command Prompt / Terminal:

   ```bash

   # (recommended) create and activate a venv
   python -m venv .venv

   # Windows:
   .venv\\Scripts\\activate

   # macOS/Linux:
   source .venv/bin/activate
   
   pip install -r requirements.txt

   ```
   
3. Open **AgriDroneRL_Main_PPO.ipynb** for the main PPO pipeline, **AgriDroneRL_Comparative.ipynb** for PPO vs DQN vs A2C comparison notebook.

4. Run all cells sequentially:
   - NDVI generation.
   - PPO training.
   - Multi-agent hybrid simulation.
   
5. Outputs (plots, GIFs, metrics) are saved to `results/`.

---

## Results & Analysis

PPO consistently achieves the highest episode returns and coverage ratios, indicating strong exploration efficiency under sparse, first-visit rewards. DQN exhibits unstable trajectories and higher revisit rates, while A2C shows moderate performance but lower sample efficiency. Overall, PPO demonstrates superior stability and vegetation-aware navigation.

---

## Limitations

- Single-drone setup (no multi-agent coordination).  
- Sparse rewards in later exploration stages.  
- No explicit safety-aware learning.  

---

## Citation

> Ayushman Mishra, *AgriDroneRL: NDVI-Based Drone Navigation using Reinforcement Learning*, github.com/aymisxx/AgriDroneRL

> Ayushman Mishra, *MicroUAV-2D: Lightweight 2D Down-Camera UAV Simulation Environment for Rapid Autonomy Prototyping*, github.com/aymisxx/MicroUAV-2D

---

**Clean, reproducible RL benchmark for agricultural drone navigation.**

---
