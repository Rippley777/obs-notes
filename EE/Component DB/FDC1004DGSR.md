# Component Documentation: FDC1004DGSR

## General Information

- **Component:** FDC1004DGSR
- **Type:** 4-Channel Capacitive Sensor
- **Manufacturer:** Texas Instruments

## Specifications

- **Supply Voltage:** 2.7 V to 3.6 V
- **Measurement Range:** ±15 pF with ±100 pF offset
- **Resolution:** 16-bit
- **Interface:** I2C
- **Conversion Time:** 15 ms per channel
- **Package:** VSSOP-10
- **Technology:** Capacitive Sensing

## Characteristics

- **Operating Temperature Range:** -40°C to 85°C
- **Noise Level:** 0.5 fF RMS
- **Sampling Rate:** 100 Hz (Typical)
- **Input Capacitance:** Up to 100 pF offset

## Applications

- Capacitive Touch Interfaces
- Liquid Level Sensing
- Proximity Detection
- Humidity Monitoring

## Pinout

1. **VDD (Power Supply)**
2. **GND (Ground)**
3. **SDA (I2C Data Line)**
4. **SCL (I2C Clock Line)**
5. **CH1 (Channel 1 Input)**
6. **CH2 (Channel 2 Input)**
7. **CH3 (Channel 3 Input)**
8. **CH4 (Channel 4 Input)**
9. **CAPDAC (Capacitive Offset DAC)**
10. **NC (No Connect)**

## Testing Instructions

### Using a Multimeter

1. **Power Verification:**
    - Check VDD and GND for proper supply voltage.
2. **I2C Line Check:**
    - Measure voltage levels on SDA and SCL; they should idle at VDD with pull-up resistors.

### Using an Oscilloscope

1. **Signal Analysis:**
    - Probe SDA and SCL to ensure proper I2C communication.
    - Observe signal integrity for noise or distortion.
2. **Capacitive Response Test:**
    - Connect known capacitive elements to channels and observe output behavior.

### Using a Capacitance Meter

1. **Channel Calibration:**
    - Attach test capacitors and verify measured values.
    - Adjust CAPDAC if necessary for offset correction.

## Usage Notes

- Use proper shielding for measurements in noisy environments.
- Place input traces away from high-voltage lines to avoid interference.
- Handle with ESD precautions.

## Practical Application Guide

### Recommended Circuit Configuration

- **Power Supply:** Use a clean 3.3 V regulated supply.
- **I2C Interface:** Include 4.7 kΩ pull-up resistors on SDA and SCL.
- **Shielding:** Use driven shields for high-sensitivity applications.

### Troubleshooting Tips

- If no measurements, verify I2C address and SDA/SCL connections.
- If readings drift, check CAPDAC settings and grounding.
- For noisy signals, add shielding or ferrite beads on signal lines.

### Safety Considerations

- Avoid exceeding the 3.6 V supply limit.
- Follow ESD-safe practices when handling.
- Maintain proper insulation in high-sensitivity environments.

## Advanced Tips & Insights

- **Noise Reduction:** Use twisted-pair cables for channel inputs.
- **Sensitivity Adjustment:** Adjust CAPDAC for varying dielectric conditions.
- **Liquid Level Sensing:** Calibrate against known fluid levels for improved accuracy.
- **Proximity Detection:** Test in target environment for best performance.

## Inventory Integration Plan

**RFID Tag ID:** TBD **Location:** Component Shelf - Capacitive Sensors

**Markdown Code:** `#fdc1004dgsr`

Scan with RFID scanner to pull up this document when needed.