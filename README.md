# Particle Physics Simulation — Charged Particle Trajectory in a Magnetic Field

This simulation models the trajectory of a charged particle moving through a uniform magnetic field, using the Lorentz force law. The result is a 3D plot of the particle's path.

## Physics

A charged particle moving through a magnetic field experiences the **Lorentz force**:

```
F = q(v × B)
```

Where:
- `q` — particle charge (Coulombs)
- `v` — particle velocity vector (m/s)
- `B` — magnetic field vector (Tesla)
- `×` — cross product

This force is always perpendicular to the velocity, so it changes the particle's direction without changing its speed. In a uniform field, this produces circular or helical motion depending on whether the velocity has a component parallel to the field.

## How It Works

The simulation uses a simple **Euler integration** loop:

1. Compute the Lorentz force: `F = q * (v × B)`
2. Compute acceleration: `a = F / m`
3. Update velocity: `v += a * dt`
4. Renormalize the xy-components of velocity to conserve total speed (corrects for numerical drift introduced by Euler integration)
5. Update position: `pos += v * dt`
6. Repeat for every time step up to `total_time`

The trajectory is stored and then rendered as a 3D matplotlib plot.

## Running the Simulation

Open `Particle_Physics_Simulation_trajectory_of particle_corrections.ipynb` in Jupyter and run the cell. You will be prompted interactively in two stages.

### Stage 1 — Choose a particle

```
Select a Particle:
Electron
Positron
Proton
Antiproton
Custom
```

The four presets have the following properties:

| Particle    | Charge (C)   | Mass (kg)   | Time step (s) | Total time (s) |
|-------------|--------------|-------------|---------------|----------------|
| Electron    | -1.6e-19     | 9.11e-31    | 1e-11         | 1e-8           |
| Positron    | +1.6e-19     | 9.11e-31    | 1e-11         | 1e-8           |
| Proton      | +1.6e-19     | 1.67e-27    | 1e-11         | 2e-7           |
| Antiproton  | -1.6e-19     | 1.67e-27    | 1e-11         | 2e-7           |

Choosing **Custom** prompts you to enter charge, mass, time step, and total time manually (use standard form, e.g. `1.6e-19`).

### Stage 2 — Advanced settings (optional)

```
Do you wish to modify starting position, velocity, and magnetic field components? (y/n)
```

Entering `y` lets you specify:
- **Initial position** — `x, y, z` in metres (comma-separated)
- **Magnetic field** — `Bx, By, Bz` in Tesla
- **Initial velocity** — `vx, vy, vz` in m/s

Entering `n` uses the defaults:

| Parameter        | Default value              |
|------------------|----------------------------|
| Position (x,y,z) | `0, 0, 0` m               |
| B field (Bx,By,Bz) | `0, 0, 0.4` T (along z)  |
| Velocity (vx,vy,vz) | `1e6, 1e6, 1e6` m/s    |

With the default field pointing along z and a velocity that has both transverse and z-components, the particle follows a **helix** — circular in the xy-plane while drifting along z.

## Output

A 3D matplotlib window showing the full trajectory, labelled in metres.
<img width="653" height="658" alt="newpositron" src="https://github.com/user-attachments/assets/cae7a383-8c16-4ec7-b973-538ac2e18f8a" />

## Requirements

```
numpy
matplotlib
```

A Tk display is required for the interactive plot window (`TkAgg` backend). When running inside Jupyter without a display (e.g. a headless server), swap the backend to `inline`:

```python
# Replace this line near the top of the notebook:
matplotlib.use('TkAgg')
# With:
%matplotlib inline
```
