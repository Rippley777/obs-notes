# Component Documentation: DRV2605LDGSR

## General Information

- **Component:** DRV2605LDGSR
- **Type:** Haptic Driver with ERM and LRA Support
- **Manufacturer:** Texas Instruments

## Specifications

- **Supply Voltage:** 2.5 V to 5.2 V
- **Output Voltage:** Up to 5.5 V
- **Interface:** I2C
- **Operating Modes:** ERM, LRA, and Waveform Sequencing
- **Waveform Library:** Preloaded with 123 haptic effects
- **Package:** VSSOP-10
- **Technology:** Haptic Feedback Driver

## Characteristics

- **Operating Temperature Range:** -40°C to 85°C
- **Standby Current:** 1 µA
- **Active Current:** 3.5 mA (Typical)
- **Drive Frequency:** 45 Hz to 300 Hz (LRA)
- **Output Current:** 300 mA Maximum

## Applications

- Tactile Feedback in Touch Interfaces
- Gaming Controllers
- Wearable Devices
- VR/AR Systems

## Pinout

1. **VDD (Supply Voltage)**
2. **GND (Ground)**
3. **SDA (I2C Data Line)**
4. **SCL (I2C Clock Line)**
5. **EN (Enable)**
6. **OUT+ (Output Positive)**
7. **OUT- (Output Negative)**
8. **IN/TRIG (Input/Trigger)**
9. **MODE (Mode Select)**
10. **NC (No Connect)**

## Testing Instructions

### Using a Multimeter

1. **Power Verification:**
    - Check VDD and GND for correct voltage level.
    - Verify continuity for ground connections.
2. **I2C Line Check:**
    - Measure voltage on SDA and SCL lines; should idle at VDD with pull-ups.

### Using an Oscilloscope

1. **Signal Analysis:**
    - Probe SDA and SCL to verify proper I2C communication.
    - Monitor OUT+ and OUT- for haptic waveform signals.
2. **Frequency Check:**
    - Measure output frequency to confirm proper LRA/ERM operation.

### Using a Vibration Sensor

1. **Output Performance:**
    - Attach an accelerometer to the actuator.
    - Run test patterns and verify vibration intensity and frequency.

## Usage Notes

- Use proper pull-up resistors for I2C communication.
- Select appropriate haptic mode based on actuator type (ERM/LRA).
- Handle with ESD precautions to avoid damage.

## Practical Application Guide

### Recommended Circuit Configuration

- **Power Supply:** Provide a clean 3.3 V or 5 V regulated supply.
- **I2C Interface:** Use 4.7 kΩ pull-up resistors for SDA and SCL.
- **Actuator Connection:** Connect ERM/LRA actuator to OUT+ and OUT-.

### Troubleshooting Tips

- If no vibration, check I2C communication and actuator wiring.
- If vibration is weak, verify actuator type and gain settings.
- Check MODE pin logic level for correct operating mode.

### Safety Considerations

- Avoid exceeding 5.5 V on VDD or OUT+.
- Ensure proper heat dissipation during continuous operation.
- Follow ESD-safe practices when handling the component.

## Advanced Tips & Insights

- **Custom Waveforms:** Use I2C commands to load custom haptic patterns.
- **Performance Optimization:** Adjust drive time and gain for different actuator types.
- **Noise Reduction:** Add decoupling capacitors near VDD.
- **Testing Automation:** Use microcontroller scripts to automate vibration tests.

## Inventory Integration Plan

**RFID Tag ID:** TBD **Location:** Component Shelf - Haptic Drivers

**Markdown Code:** `#drv2605ldgsr`

Scan with RFID scanner to pull up this document when needed.