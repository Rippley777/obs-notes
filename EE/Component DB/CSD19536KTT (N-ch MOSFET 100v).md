# Component Documentation: CSD19536KTT

## General Information

- **Component:** CSD19536KTT
- **Type:** N-Channel MOSFET
- **Manufacturer:** Texas Instruments

## Specifications

- **Drain-Source Voltage (Vds):** 100 V
- **Continuous Drain Current (Id) @ 25°C:** 84 A
- **Rds(on) @ Vgs = 10 V:** 4.3 mΩ
- **Gate-Source Voltage (Vgs):** ±20 V
- **Package:** TO-220-3
- **Technology:** MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor)
- **FET Feature:** Logic Level Gate Drive

## Characteristics

- **Power Dissipation (Pd) Max:** 170 W
- **Operating Temperature Range:** -55°C to 175°C
- **Gate Charge (Qg) @ 10V:** 65 nC
- **Threshold Voltage (Vth):** 2.3 V - 3.7 V

## Applications

- High-Efficiency Power Conversion
- Motor Drivers
- DC-DC Converters
- Load Switching

## Pinout

1. **Gate (G)**
2. **Drain (D)**
3. **Source (S)**

## Testing Instructions

### Using a Multimeter

4. **Diode Test Mode:**
    - Place the positive lead on the Drain and the negative lead on the Source.
    - A reading indicates the body diode is present.
    - Reverse the leads; it should read OL (Open Line) if functional.
5. **Gate Test:**
    - Place positive lead on Gate and negative on Source; it should charge and cause the Drain-Source to conduct.
    - Discharge by connecting Gate to Source.

### Using an Oscilloscope

6. **Gate Drive Test:**
    - Apply a square wave to the Gate with the Source grounded.
    - Observe the Drain signal; it should mirror the Gate waveform if functional.
7. **Rds(on) Measurement:**
    - Apply a known current and measure voltage drop; divide voltage by current to find Rds(on).

## Usage Notes

- Ensure proper heat sinking when operating near max current.
- For switching applications, ensure gate driver can handle the gate charge (Qg).
- Static-sensitive: handle with ESD precautions.

## Practical Application Guide

### Recommended Circuit Configuration

- **Power Supply:** Use a stable 12 V supply with a 0.1 µF ceramic capacitor close to the gate driver.
- **Gate Resistor:** Use a 10 Ω resistor for testing and adjust based on application requirements.
- **Grounding:** Implement a solid ground plane for consistent performance.

### Troubleshooting Tips

- If transistor doesn't switch, verify gate-source voltage.
- If excessive heating occurs, check Rds(on) and ensure correct load conditions.
- Check for proper polarity and connection of leads.

### Safety Considerations

- Always discharge the gate to source after testing.
- Handle carefully to avoid static damage.
- Monitor device temperature during prolonged testing.

## Advanced Tips & Insights

- **Thermal Management:** Use thermal paste and adequate heat sinking when running high current.
- **Gate Driver Selection:** Ensure the gate driver can supply the required gate charge (Qg) rapidly to avoid slow switching.
- **Parasitic Inductances:** Minimize lead lengths and use twisted pairs for long connections to reduce EMI.
- **ESD Protection:** Use transient-voltage-suppression (TVS) diodes if working in environments prone to electrostatic discharge.
- **Frequency Optimization:** For switching applications, evaluate switching losses at different frequencies to find an optimal balance.

## Inventory Integration Plan

**RFID Tag ID:** TBD **Location:** Component Shelf - MOSFETs

**Markdown Code:** `#csd19536ktt`

Scan with RFID scanner to pull up this document when needed.