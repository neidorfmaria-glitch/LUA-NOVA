# LUA NOVA

### Numerical Simulation of Orbital Trajectories

LUA NOVA is an ongoing independent research project exploring how numerical integration methods affect the accuracy and stability of simulated orbital trajectories.

I am developing a Python-based simulation engine to investigate orbital dynamics, compare numerical methods, and explore approaches that balance computational efficiency with accuracy.

> **Status:** Work in progress — active development

---

## Research Question

**How does the choice of numerical integration algorithm affect the accuracy and stability of simulated orbital trajectories?**

The project currently focuses on comparing:

* **Euler's method**
* **Fourth-order Runge-Kutta (RK4)**
* **Hybrid numerical approaches**

The long-term goal is to extend the simulation framework toward more complex orbital dynamics and **N-body systems**.

---

## Current Findings

Initial experiments show that **RK4 produces substantially lower numerical error and energy drift than Euler integration**, particularly over long simulations.

I am also developing a **hybrid approach** designed to balance the accuracy of higher-order integration with computational efficiency.

Results are evaluated through numerical error analysis and visualizations of simulated trajectories and system behavior.

---

## Methodology

The simulation engine is being developed in **Python** and uses numerical integration to solve the differential equations governing orbital motion.

The current workflow includes:

1. Define the orbital system and initial conditions.
2. Numerically integrate the equations of motion.
3. Simulate the trajectory over many time steps.
4. Compare Euler and RK4 integration.
5. Measure numerical error and energy drift.
6. Visualize and analyze the results.
7. Develop and evaluate improved integration strategies.

---

## Results

### Euler vs. RK4

Initial simulations indicate that RK4 maintains orbital stability and energy conservation significantly better than Euler integration over long time intervals.

*Figures and quantitative results will be added as the project develops.*

---

## Technologies

* Python
* Numerical Methods
* Differential Equations
* Computational Physics
* Data Visualization
* Scientific Computing

---

## Future Work

The project is currently under active development.

Planned extensions include:

* Refining the hybrid integration method
* Expanding error analysis
* Testing different orbital configurations
* Improving computational efficiency
* Extending the engine toward **N-body simulations**
* Investigating the behavior of numerical methods in more complex gravitational systems

---

## About the Project

LUA NOVA is an independent research project developed to explore computational approaches to orbital dynamics and numerical simulation.

This repository documents the development process, experiments, results, and ongoing research.

**Status: 🚧 Active development**
