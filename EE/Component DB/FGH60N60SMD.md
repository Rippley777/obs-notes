# Component Documentation: FGH60N60SMD

## General Information

- **Component:** FGH60N60SMD
- **Type:** N-Channel IGBT (Insulated Gate Bipolar Transistor)
- **Manufacturer:** ON Semiconductor

## Specifications

- **Collector-Emitter Voltage (Vce):** 600 V
- **Continuous Collector Current (Ic) @ 25°C:** 60 A
- **Gate-Emitter Voltage (Vge):** ±20 V
- **Collector-Emitter Saturation Voltage (Vce(sat)):** 2.1 V @ 60 A
- **Switching Frequency:** Up to 100 kHz
- **Power Dissipation:** 300 W
- **Package:** TO-247
- **Technology:** Field-Stop IGBT

## Characteristics

- **Operating Temperature Range:** -55°C to 150°C
- **Gate Charge (Qg) @ 15V:** 120 nC
- **Input Capacitance (Ciss):** 3,500 pF
- **Turn-On Delay Time (td(on)):** 40 ns
- **Turn-Off Delay Time (td(off)):** 250 ns

## Applications

- Inverter Circuits
- Motor Drives
- Welding Equipment
- Power Factor Correction (PFC) Circuits

## Pinout

1. **Gate (G)**
2. **Collector (C)**
3. **Emitter (E)**

## Testing Instructions

### Using a Multimeter

4. **Diode Test Mode:**
    - Place the positive lead on the Collector and the negative lead on the Emitter.
    - A reading of ~0.5-0.7 V indicates a functioning body diode.
    - Reverse the leads; should read OL (Open Line).
5. **Gate Test:**
    - Place positive lead on Gate and negative on Emitter; it should charge and cause Collector-Emitter conduction.
    - Discharge by connecting Gate to Emitter.

### Using an Oscilloscope

6. **Switching Test:**
    - Apply a square wave to the Gate with the Emitter grounded.
    - Monitor Collector signal; it should mirror the gate waveform with minimal delay.
7. **Switching Loss Measurement:**
    - Measure the turn-on and turn-off times under load.

## Usage Notes

- Ensure proper heat sinking to manage thermal dissipation.
- Drive the gate with appropriate voltage levels for efficient switching.
- Handle with ESD precautions due to gate sensitivity.

## Practical Application Guide

### Recommended Circuit Configuration

- **Gate Drive:** Use a dedicated gate driver with a 10-Ω resistor.
- **Snubber Circuit:** Include RC snubber across Collector-Emitter to reduce voltage spikes.
- **Thermal Management:** Use thermal interface material with heat sink.

### Troubleshooting Tips

- If transistor does not switch, verify gate signal and gate-emitter resistor.
- If excessive heat, check for correct Rg and power dissipation.
- For switching anomalies, inspect driver output waveform.

### Safety Considerations

- Avoid exceeding Vce or Vge ratings.
- Ensure proper isolation in high-voltage circuits.
- Follow ESD-safe procedures when handling.

## Advanced Tips & Insights

- **Thermal Efficiency:** Utilize copper planes on PCB for improved heat dissipation.
- **Switching Performance:** Select gate resistor to balance switching speed and noise.
- **Parasitic Inductance:** Keep gate wiring short to minimize parasitic effects.
- **Parallel Configuration:** Use matched devices and separate gate resistors for parallel operation.

## Inventory Integration Plan

**RFID Tag ID:** TBD **Location:** Component Shelf - IGBTs

**Markdown Code:** `#fgh60n60smd`

Scan with RFID scanner to pull up this document when needed.