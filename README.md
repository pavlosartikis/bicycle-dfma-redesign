# Redesigned City Commuter Bicycle — DFMA & SolidWorks Project

A full Design for Manufacture and Assembly (DFMA) project: teardown and analysis of a commercial Apollo commuter bicycle, followed by a ground-up redesign featuring a custom dual-spring rear suspension system, validated with FEA in SolidWorks Simulation.


---

## The Project

The original bicycle (Apollo Elusion, ~£180–250) was a mass-produced step-through commuter bike with an 18-speed derailleur drivetrain, rim brakes, and no rear suspension. After a full teardown and bill of materials analysis, I redesigned it from scratch with manufacturability and assembly efficiency as the primary drivers.

---

## Part 1 — Teardown & Analysis

The bicycle was fully disassembled and documented:

- **Sub-assembly identification** — 10 major sub-assemblies catalogued (drivetrain, braking, headset, wheels, seat, handlebars, forks, pedals, etc.)
- **Bill of Materials** — every component documented with material, manufacturing process, and critical function
- **Assembly efficiency analysis** — identified bottlenecks including complex gear indexing, cable routing, and secondary finishing (painting)
- **Manufacturing process review** — stamping, cold forming, tube bending, welding, injection moulding

**Key findings:** The 18-speed drivetrain and rim brake system introduced the most assembly complexity. The lack of any suspension was a comfort and performance limitation. Rim brakes degraded the structural wheel over time by wearing the aluminium sidewall.

---

## Part 2 — Redesign

### Design Philosophy

The redesign applied DFMA principles throughout:
- Minimise component and fastener count
- Use standard off-the-shelf parts wherever possible
- Enable modular, parallel assembly
- Eliminate secondary finishing processes (painting)
- Prioritise assembly accessibility

### Key Design Decisions

#### Drivetrain — 18-speed → Single-speed
The complex multi-gear system (derailleurs, cassette, indexed shifters, cabling) was replaced with a single-speed setup.

| Aspect | Original (18-speed) | Redesign (Single-speed) |
|---|---|---|
| Component count | High | Very low |
| Assembly time | High (indexing required) | Very low |
| Tooling complexity | High | Simple |
| DFMA suitability | Poor | Excellent |

#### Braking — Rim brakes → Mechanical disc brakes
Disc brakes locate the wear surface at the hub-mounted rotor rather than the structural wheel rim, ensuring consistent wet-weather stopping power and replacing a wear-and-replace structural component with a cheap, serviceable rotor.

#### Suspension — Custom dual-spring rear suspension (novel design)

This was the core innovation of the project. Three concepts were evaluated:

| Concept | Description | Verdict |
|---|---|---|
| A — Linkage-based with internal tuned mass damper (TMD) | Triangulated rear triangle, TMD inside frame tube | TMD rejected — rider-specific calibration incompatible with mass production |
| B — Vertical linear rail | Rear triangle slides vertically instead of pivoting | Rejected — requires custom rails, tight tolerances, expensive seals |
| C — Integrated hydraulic damper | Custom damper built into frame | Rejected — requires clean-room assembly, specialist tooling |

**Selected:** A simplified triangulated single-pivot rear suspension with a **dual-spring system** replacing the TMD.

**Why dual-spring over single-shock:**

A single shock applies the full impact load to one bolt. With a design load of 2000 N (representing a 2g dynamic impact for a 100 kg system) and a standard M6 fastener (stress area = 20.1 mm²):

- **Single shock:** σ = 2000 / 20.1 = **99.5 MPa**
- **Dual spring (load shared):** σ = 1000 / 20.1 = **49.8 MPa**

The dual-spring arrangement **halves the shear stress** on the mounting hardware, doubles the Factor of Safety, and allows standard lower-grade fasteners. Using two springs with different spring rates also achieves a progressive (non-linear) force-deflection curve without custom hydraulic valving.

#### Frame material — Chromoly steel → Chrome stainless steel
Stainless steel forms a self-repairing passive oxide layer, **eliminating the entire paint shop** from the production process (degreasing, priming, painting, curing). This reduces cycle time, removes VOC filtration requirements, and lowers cost, while providing equivalent structural performance (E = 200 GPa, yield strength = 172 MPa).

#### Handlebars — Telescopic height adjustment
A simple telescopic inner/outer tube design replaces a multi-piece folding hinge mechanism, reducing part count at the handlebar assembly from multiple brackets and pivot pins to two concentric tubes with a spring-loaded locking pin.

---

## FEA Structural Validation (SolidWorks Simulation)

A static FEA was conducted on the redesigned frame to validate structural integrity under a representative rider load.

**Setup:**
- Software: SolidWorks Simulation
- Material: Chrome Stainless Steel (linear elastic isotropic)
- Yield strength: 172 MPa | E = 200 GPa
- Mesh: Blended curvature-based, 44,790 nodes / 24,443 elements, 93.7% aspect ratio < 3
- Load: 900 N applied at seat tube/top tube interface (representative 95th percentile male rider)
- Fixtures: Fixed geometry at rear dropouts and head tube interface

**Results:**

| Metric | Result | Limit / Target | Status |
|---|---|---|---|
| Max Von Mises stress | 128 MPa | 172 MPa (yield) | ✅ Safe |
| Max displacement | 0.117 mm | — | ✅ Highly rigid |
| Min Factor of Safety | 1.35 | > 1.0 (static) | ✅ Safe |
| Max equivalent strain | 0.00026 (0.026%) | ~0.2% (yield) | ✅ 13% of limit |

**Critical location:** The seat tube / bottom bracket junction governs — expected due to the cantilevered rear triangle geometry. This justifies prioritising weld quality at this joint in manufacture.

**Key insight:** The FoS of 1.35 under static loading confirms the dual-spring suspension is essential — dynamic impacts (potholes, kerbs) can multiply forces by 2–3×, which would approach the yield limit without the suspension absorbing peak loads before they reach the frame.

---

## Files

```
bicycle-dfma-redesign/
├── README.md
├── report/
│   └── FINAL_REPORT.pdf             ← Full 116-page report
├── solidworks/
│   └── (SolidWorks assembly files)  ← Add your .SLDASM files here
├── fea/
│   ├── von_mises_stress.png         ← Stress contour plot
│   ├── displacement.png             ← Displacement result
│   ├── factor_of_safety.png         ← FoS distribution
│   └── strain.png                   ← Equivalent strain
└── design/
    ├── bicycle_right_view.png       ← SolidWorks renders
    ├── bicycle_angled_view.png
    └── suspension_concepts.png      ← Concept sketches
```

---

## Tools

- SolidWorks (CAD + FEA Simulation)
- DFMA methodology (Boothroyd, Dewhurst & Knight)

---

## Key Takeaways

- Systematic DFMA analysis of an existing product reveals specific, quantifiable manufacturing bottlenecks — not just general observations
- Suspension concept selection is fundamentally a manufacturing problem as much as a mechanical one; novel ideas fail DFMA if they require non-standard processes or rider-specific calibration
- Distributing a load across two symmetric springs halves bolt shear stress — a simple calculation with a large structural benefit
- Material selection upstream (stainless vs carbon steel) can eliminate entire downstream manufacturing stages (painting), saving cost and time more effectively than optimising the paint process itself
- A FoS of 1.35 under static loading is safe, but highlights exactly where dynamic loading becomes critical — and justifies the suspension design decision quantitatively
