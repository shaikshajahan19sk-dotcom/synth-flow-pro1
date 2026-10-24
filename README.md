# Synth-Flow Pro

**A browser-based digital twin and energy-management simulator for a hypothetical hydrogen-hybrid vehicle.**

Synth-Flow Pro models how a hydrogen-derived power source (a LOHC supply abstraction feeding a fuel cell) and a structural "Smart Skin" battery share the load of a vehicle. It lets you compare five energy-management controllers on identical scenarios and inspect every decision. It started as a first-year B.Tech ECE college competition project.

> **Simulation only.** Every number is computed locally from hypothetical parameters. Nothing here controls or connects to real hardware, and the model is not validated, not safety-certified, and not a specification of any real vehicle. The LOHC block is a mathematical abstraction, not dehydrogenation chemistry. The Smart Skin battery is a conceptual model and proves nothing about physical feasibility.

## Run it

It is a single self-contained HTML file with no build step and no dependencies.

1. Download `synth-flow-pro.html` and open it in any modern browser (desktop or mobile).
2. Or host it free with GitHub Pages: rename the file to `index.html`, then go to **Settings > Pages** and publish from your main branch.

The default demo starts automatically (hydrogen 75%, SOC 80%, battery 28 °C, 300 W demand, Synth-Flow controller, 120 s).

## What it does

- **Deterministic engine**: 1-second steps, SI units internally, identical inputs always give identical results.
- **Subsystems**: LOHC supply abstraction (availability and warm-up), fuel cell (ramp limits, minimum stable output, illustrative efficiency), battery (SOC, voltage sag, I²R loss, thermal model and derating, SOC protection, charge and discharge limits).
- **Power balance every step**: `P_fc + P_batt = P_demand - P_unmet + P_surplus`. Regenerative braking is negative demand; anything the battery cannot accept is reported as surplus, never silently dropped. A live indicator flags any imbalance.
- **Five controllers** (all rule-based heuristics, no trained AI): fixed threshold, fuel-cell priority, battery priority, demand-preview heuristic, and Synth-Flow condition-aware control.
- **Plant limits sit after the controller**, so no controller can bypass battery or fuel-cell limits.
- **Command Center**: animated power-flow diagram driven by the computed powers, gauges, charts, warnings, clickable subsystem details, and a "Why did the controller do this?" panel (what it saw, the active constraint, the action, the reason, the rejected alternative).
- **Controller Lab**: runs all five controllers on one or all scenarios with the same start state and settings, shows unmet energy, fuel-cell and battery energy, regen recovered, SOC range, peak temperature, switches, and failed runs. Results are copyable as CSV or JSON.
- **9 scenarios** and **4 injectable faults** (hydrogen drop, battery overheat, load spike, stale controller data), with live Start, Pause, Step, Run to end, Reset, and a software E-STOP.

## The research hypothesis

The Synth-Flow controller estimates a short-term fuel-cell supply shortfall from previewed demand and hydrogen-derived power, compares it with what the battery may safely deliver right now (including thermal derating and SOC reserve), and then pre-charges, shares, or follows demand. This is a **testable hypothesis, not an established invention**. It is not hardcoded to win: use the Controller Lab and report whatever comes out, including scenarios where a simpler controller does as well or better.

## Not implemented yet

Vehicle-dynamics model (drag, rolling resistance, gradient, speed), custom scenario editor and saved scenarios, the remaining planned scenarios, parameter sweeps and sensitivity analysis, chart zoom and hover tooltips, Sankey and exploded views, beginner/engineering mode switch, sensor-bias/noise/temperature-sensor faults, patent notebook form, project documentation pages, and file downloads (shown as copyable text instead). No automated test suite is included yet.

## Patent note

Combining LOHC, fuel cells, batteries, and an energy controller is not automatically novel or patentable. Do a proper prior-art search first: [IPIndia](https://iprsearch.ipindia.gov.in/PublicSearch/), [Google Patents](https://patents.google.com/), [WIPO PATENTSCOPE](https://patentscope.wipo.int/), [Espacenet](https://worldwide.espacenet.com/). This repository makes no novelty or legal claims.

## Safety

Educational software only. The E-STOP button halts the simulation clock; it is not a physical emergency stop. Do not use any part of this for real vehicle control.

## Roadmap

Vehicle dynamics and drive cycles, scenario editor, parameter sweeps, richer fault models, tooltips and zoom, and a low-voltage educational hardware prototype to compare against the model.

## Contributors and license

Add your team and college here, and choose a license (MIT is a common choice for student projects).
