# Satellite-Attitude-Control-Using-Reaction-Wheels-
IITI Soc - DEIMoS - PS 2  - Satellite attitude control using reaction wheels - End Evalution


Design and simulation of a closed-loop attitude control system for a 3U CubeSat using reaction wheels, covering rigid-body dynamics modeling, PID controller design, and Simulink-based verification across multiple maneuver scenarios.

## Team

| Name    | Role |
|B.Nandini| Team Lead |
|M.Charan | Member — Mechanical Engineering, IIT Indore |

## Overview

The goal of this project is to control the orientation (attitude) of a CubeSat using reaction wheels as actuators. Physical parameters of the spacecraft — mass, inertia tensor, and geometry — were derived directly from a CAD model rather than assumed, giving the controller design a realistic, asymmetric mass distribution to work against. A PID controller was designed and tuned, then validated in Simulink under two representative scenarios, and the results were analyzed and post-processed in MATLAB.

## Repository Structure

```
├── MATLAB CODE                                          # Post-processing & analysis script
├── Satellite_Attitude_Control_Scenario_A__.slx.zip       # Simulink model — Scenario A
├── Satellite_Attitude_Control_Scenario_B__.slx.zip       # Simulink model — Scenario B
├── satellite designing (CAD).step                        # 3U CubeSat CAD model
├── scenario A.jpeg                                        # Result plots — Scenario A
├── scenario B.jpeg                                        # Result plots — Scenario B
├── simulink.jpeg                                          # Simulink model overview
├── VIDEO (PS2 plots and simulation).mp4                   # Simulation walkthrough
└── Final_Report__DEIMoS___PS2.pdf                          # Full project report
```

## Methodology

### 1. Spacecraft Model
- Modeled as a 3U CubeSat, Aluminium 6061 structure.
- Mass properties and the full inertia tensor — including an off-diagonal cross-coupling term arising from an asymmetric solar panel — were extracted directly from the CAD model (`satellite designing (CAD).step`), rather than approximated as a diagonal/symmetric body.
- Rotational dynamics follow Euler's equations with gyroscopic (cross-axis) coupling, so motion about one axis affects the others — a more realistic model than a decoupled single-axis approximation.

### 2. Controller Design
- A PID controller was designed for the reaction-wheel-driven attitude loop using classical second-order system tuning (relating desired rise time / overshoot to natural frequency and damping ratio).
- An early numerical instability caused by the small inertia of the reaction wheel relative to the spacecraft body was identified and resolved during tuning.
- Actuator torque limits were enforced to keep the simulation physically realistic (visible as saturation in the control torque plots).

### 3. Simulation & Scenarios
Two scenarios were built and simulated in Simulink:
- **Scenario A** — Large-angle slew maneuver (commanded reorientation, e.g. a 45° attitude step).
- **Scenario B** — Disturbance rejection (holding attitude against an external disturbance torque).

Each Simulink model (`.slx`, zipped) implements the PID controller, current-loop/DC-motor-driven reaction wheel, and the disturbance environment feeding the rigid-body dynamics block.

### 4. Analysis
The `MATLAB CODE` script takes the logged Simulink outputs (`theta`, `error`, `torque`, `wheelSpeed`, `tout`) and computes standard control performance metrics:
- Rise time (10%–90%)
- Peak time and overshoot
- 2% settling time
- Steady-state and RMS error
- Torque and wheel-speed extremes

It also generates annotated plots (attitude response, error, control torque, wheel speed, and a combined 4-panel summary) exported as high-resolution PNGs.

## Results

Result plots for each scenario are included as `scenario A.jpeg` and `scenario B.jpeg`, with a Simulink model overview in `simulink.jpeg`. A recorded walkthrough of the simulation and result plots is available in the video file. Full quantitative results, methodology, and discussion are documented in the final report.

## How to Run

**Simulink models:**
1. Unzip the desired scenario (`Scenario A` or `Scenario B`).
2. Open the `.slx` file in Simulink (R2021a or later recommended).
3. Run the simulation — this logs `theta`, `error`, `torque`, `wheelSpeed`, and `tout` to the MATLAB workspace.

**Analysis script:**
1. After running a Simulink scenario (so the workspace variables above exist), open `MATLAB CODE` in MATLAB.
2. Run the script to print the performance summary and export the annotated result plots as PNGs.

**CAD model:**
- `satellite designing (CAD).step` can be opened in any standard CAD tool (Fusion 360, SolidWorks, etc.) to inspect the 3U CubeSat geometry and mass distribution used to derive the inertia tensor.

## Documentation

- 📄 **Final Report** — full write-up of modeling, controller design, and results (`Final_Report__DEIMoS___PS2.pdf`)
- 🎥 **Simulation Video** — plots and simulation walkthrough (`VIDEO (PS2 plots and simulation).mp4`)
