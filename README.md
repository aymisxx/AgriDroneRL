# AgriDroneRL

### NDVI-Based Drone Navigation using Reinforcement Learning  
**(PPO vs DQN vs A2C: A Comparative Study)**

**Authors:**

- **Ayushman Mishra**: https://github.com/aymisxx  
- **Sanskar S. Patil**: https://github.com/sanskar-sunil-patil  
- **Kshitij Gupta**: https://github.com/kgupt0310  

---

## Project Overview

**AgriDroneRL** investigates vision-based autonomous drone navigation over agricultural fields using reinforcement learning. A fixed-altitude drone observes a local 128×128 vegetation patch extracted from a satellite-derived NDVI proxy and selects discrete motion actions to maximize informative field coverage.

---

## Environment Design

- **Vegetation Map:** VARI-based NDVI proxy computed from RGB satellite imagery, normalized to [0, 1].  
- **Observation:** 128×128 local vegetation window, single-channel image `(1, 128, 128)`.  
- **Action Space:** Discrete(4) - up, right, down, left (boundary-clamped).  
- **Reward:** NDVI value on first visit to a cell, zero on revisits.  
- **Episodes:** Fixed-length, SB3-compatible.

---

## Algorithms Compared

- PPO (Proximal Policy Optimization)  
- DQN (Deep Q-Network)  
- A2C (Advantage Actor-Critic)  

All algorithms share the same environment, episode length, and evaluation pipeline.

---

## Evaluation Metrics

- Episode return  
- Unique visited cells  
- Coverage ratio  
- Mean and median NDVI of visited cells  

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

1. Place a satellite image in `data/field_satellite.jpg`
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
   - NDVI generation
   - PPO training
   - Multi-agent hybrid simulation
5. Outputs (plots, GIFs, metrics) are saved to `results/`

---
## Results & Analysis

PPO consistently achieves the highest episode returns and coverage ratios, indicating strong exploration efficiency under sparse, first-visit rewards. DQN exhibits unstable trajectories and higher revisit rates, while A2C shows moderate performance but lower sample efficiency. Overall, PPO demonstrates superior stability and vegetation-aware navigation.

---

## Limitations

- Single-drone setup (no multi-agent coordination)  
- Sparse rewards in later exploration stages  
- No explicit safety-aware learning  

---

## Citation

> Mishra, A., Patil, S. S., Gupta, K., *AgriDroneRL: NDVI-Based Drone Navigation using Reinforcement Learning*, github.com/aymisxx/AgriDroneRL

---

**Clean, reproducible RL benchmark for agricultural drone navigation.**