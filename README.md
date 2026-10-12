# 5V-DC-DC-Buck-Converter 41.4mmx23.6mm
10–15V Input | 5V/1A Output | LTspice Simulation &amp; Altium PCB Design
<img width="907" height="536" alt="Buck_Topview" src="https://github.com/user-attachments/assets/5a2a8996-0a52-416c-9b14-5e5af8264ecb" />

**LTspice Simulation & Altium PCB Design**

Designed a non-synchronous DC-DC buck converter using the Analog Devices LT1375 to step a 10–15V DC input down to a regulated 5V output at up to 1A. I selected the electrical components, simulated and optimized the circuit in LTspice, and designed a two-layer SMD PCB in Altium Designer.

**Project Status:** LTspice simulations, schematic design, PCB layout, and routing completed. The PCB has not been physically manufactured or tested.

## Design Specifications

| Parameter | Value |
|---|---|
| Input Voltage | 10–15V DC |
| Output Voltage | 5V DC |
| Maximum Output Current | 1A |
| Output Power | 5W |
| Regulator | LT1375CS8#PBF |
| Switching Frequency | ~500 kHz |
| PCB | 2-layer SMD |
| Software | LTspice, Altium Designer |

## 1. Circuit Design

I started by researching buck converter operation and selecting components based on the input voltage range, output requirements, and manufacturer datasheets.

The design uses an LT1375 switching regulator, a 15 µH power inductor, a Schottky diode, input/output filtering capacitors, and a feedback network to regulate the output voltage.

**Key Components**

| Component | Selection |
|---|---|
| Regulator | LT1375CS8#PBF |
| Inductor | 15 µH, Bourns SRP1038A-150M (Altium design) |
| Main Diode | SS2040FL-R1-00001 |
| BOOST Diode | 1N4148W-7-F |
| Input Capacitor | 22 µF |
| Output Capacitor | 100 µF |
| Feedback Resistors | 5.36 kΩ / 4.99 kΩ |
| Compensation | 1 kΩ + 3.3 nF |
| Output Capacitor Series Resistor | 0.05 Ω |

## 2. LTspice Simulation & Optimization

I created an initial buck converter circuit (V1) in LTspice and compared its output voltage ripple against the manufacturer's LT1375 reference circuit.

V1 produced more output ripple than the reference, so I investigated how output capacitor ESR and feedback compensation affected the circuit's performance.

For V2, I decreased the modeled output capacitor ESR from 0.1 Ω to 0.05 Ω and added a 1 kΩ resistor to the compensation network.

### Simulation Results

All three configurations were compared at 15V input with a 5 Ω load, using the 8–10 ms steady-state measurement interval.

| Measurement | Reference | V1 | V2 |
|---|---:|---:|---:|
| Average Output | 5.01499V | 5.01525V | 5.01524V |
| Maximum Output | 5.03242V | 5.03798V | 5.02700V |
| Minimum Output | 4.99729V | 4.99226V | 5.00336V |
| **Peak-to-Peak Ripple** | **35.138 mV** | **45.722 mV** | **23.639 mV** |

**Results:**
- 48.3% reduction in simulated output ripple compared with V1.
- 32.7% reduction in simulated output ripple compared with the LT1375 reference circuit.

Reducing the modeled capacitor ESR lowered the ESR-related ripple contribution, while the compensation resistor modified the feedback-loop response. The independent effect of each modification has not yet been fully isolated.

## 3. Altium Schematic & PCB Design

After completing the LTspice optimization, I transferred the circuit design into Altium Designer using manufacturer-specific SMD components and footprints.

I designed a two-layer PCB with the following considerations:

- **Component Placement:** Grouped the LT1375, input capacitor, Schottky diode, BOOST circuitry, and inductor to reduce switching-path lengths.
- **Power Routing:** Used 25 mil target trace widths for major power connections and approximately 10 mil for low-current feedback and compensation signals.
- **Ground Plane:** Created a Bottom Layer GND polygon pour and connected ground pads using short traces and vias.
- **Feedback Routing:** Separated sensitive feedback connections from the switching node where possible.
- **PCB Design:** Added input/output connectors, component designators, voltage labels, and a custom board outline.

Completed schematic validation, PCB routing, and design-rule checks under the project's configured rules.

## 4. Project Files

| Folder | Contents |
|---|---|
| [Altium](Altium/) | Altium schematic, PCB layout, project files, and supporting libraries |
| [LTSpice](LTSpice/) | Reference, V1, and V2 LTspice simulations |
| [Results](Results/) | Measurement logs, ripple comparison, BOM, and design-rule reports |
| [Screenshots](Screenshots/) | Schematics, voltage waveforms, ripple graphs, PCB layouts, and 3D renderings |
| [Documentation](Documentation/) | Engineering calculations and design documentation |

## 5. Engineering Results & Limitations

The optimized circuit achieved **23.639 mV peak-to-peak simulated output ripple**, demonstrating lower ripple than both the initial design and manufacturer's reference under the tested conditions.

The PCB schematic and routing have been completed in Altium, but the physical components and board have not been tested.

Additional validation is required to confirm the effective output capacitance, actual ESR, control-loop stability, component thermal performance, and PCB manufacturing clearances. In particular, the current DRC result was obtained under modified clearance rules, which require fabrication-specific review before manufacturing.

## 6. Future Improvements

- Validate realistic capacitor and inductor characteristics across operating conditions.
- Verify load-transient response and converter efficiency.
- Review the PCB against manufacturer-supported fabrication rules.
- Manufacture, assemble, and electrically test the PCB if the design proceeds to hardware implementation.
