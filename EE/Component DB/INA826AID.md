# Component Documentation: INA826AID

## General Information

- **Component:** INA826AID
- **Type:** Instrumentation Amplifier
- **Manufacturer:** Texas Instruments

## Specifications

- **Supply Voltage (Vcc):** 2.7 V to 36 V
- **Input Offset Voltage:** 150 µV (Max)
- **Gain Range:** 1 to 1000 (Set by External Resistor)
- **CMRR (Common-Mode Rejection Ratio):** 100 dB
- **Bandwidth:** 1.2 MHz @ Gain = 1
- **Input Bias Current:** 25 nA (Typ)
- **Package:** SOIC-8
- **Technology:** Precision Analog

## Characteristics

- **Operating Temperature Range:** -40°C to 125°C
- **Slew Rate:** 2 V/µs
- **Output Swing:** Rail-to-Rail
- **Noise:** 10 nV/√Hz

## Applications

- Sensor Signal Conditioning
- Medical Instrumentation
- Data Acquisition Systems
- Industrial Process Controls

## Pinout

1. **Rg (Gain Resistor)**
2. **V+ (Positive Supply)**
3. **V- (Negative Supply / Ground)**
4. **REF (Reference Input)**
5. **VO (Output)**
6. **IN+ (Non-Inverting Input)**
7. **IN- (Inverting Input)**
8. **Rg (Gain Resistor)**

## Testing Instructions

### Using a Multimeter

1. **Continuity Check:**
    - Check between V+ and V- for short circuits.
    - Check that Rg connections are intact and match expected resistor values.
2. **Offset Voltage Measurement:**
    - Apply zero input signal and measure output; should be near the REF input level.

### Using an Oscilloscope

1. **Signal Integrity Test:**
    - Apply a known sinusoidal input.
    - Confirm the amplified output follows the input with the correct gain.
2. **Noise Measurement:**
    - Observe noise floor and compare against datasheet specifications.

## Usage Notes

- Use precision resistors for gain setting to maintain accuracy.
- Maintain a clean ground reference for low-noise operation.
- Bypass capacitors recommended close to power pins.

## Practical Application Guide

### Recommended Circuit Configuration

- **Power Supply:** Dual ±5 V or single 5 V supply.
- **Gain Resistor (Rg):** Calculate with Rg = 50 kΩ / Gain.
- **Input Filtering:** Optional low-pass filter on inputs to reduce noise.

### Troubleshooting Tips

- If output is saturated, check input signal amplitude and REF pin.
- Unexpected noise may indicate poor ground reference.
- Ensure gain resistor is within the recommended range.

### Safety Considerations

- Avoid exceeding input voltage ratings.
- Handle with proper ESD precautions.
- Confirm correct power supply polarity.

## Advanced Tips & Insights

- **Stability:** For high gains, add a small capacitor across the gain resistor.
- **Input Protection:** Series resistors can protect against transient voltages.
- **Thermal Management:** Ensure ambient temperature stays within operating limits.
- **Noise Optimization:** Shield input leads to minimize electromagnetic interference (EMI).

## Inventory Integration Plan

**RFID Tag ID:** TBD **Location:** Component Shelf - Instrumentation Amplifiers

**Markdown Code:** `#ina826aid`

Scan with RFID scanner to pull up this document when needed.