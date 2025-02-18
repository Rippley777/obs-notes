# Component Documentation: CC2652P1FRGZR

## General Information

- **Component:** CC2652P1FRGZR
- **Type:** Wireless MCU with Integrated Power Amplifier
- **Manufacturer:** Texas Instruments

## Specifications

- **Wireless Standards:** Zigbee, Thread, Bluetooth 5.1, IEEE 802.15.4
- **Supply Voltage:** 1.8 V to 3.8 V
- **Processor Core:** ARM Cortex-M4F
- **Flash Memory:** 352 KB
- **RAM:** 80 KB
- **RF Output Power:** Up to +20 dBm
- **Package:** VQFN-48
- **Technology:** Low-Power Wireless Communication

## Characteristics

- **Operating Temperature Range:** -40°C to 85°C
- **Transmit Current (Tx @ +20 dBm):** 115 mA
- **Receive Current:** 6.9 mA
- **Sleep Current:** 0.9 µA

## Applications

- Smart Home and Building Automation
- Industrial IoT Networks
- Wireless Sensor Networks
- Remote Controls and Gateways

## Pinout (Selected Pins)

1. **VCC (Power Supply)**
2. **GND (Ground)**
3. **RF_P/N (Differential RF Output)**
4. **DIO0-DIO31 (Digital I/O Pins)**
5. **SWCLK (SWD Clock)**
6. **SWDIO (SWD Data I/O)**
7. **RESET (Hardware Reset)**
8. **TXD/RXD (UART Communication)**

## Testing Instructions

### Using a Multimeter

1. **Power Verification:**
    - Measure voltage at VCC and GND to ensure proper supply.
2. **Continuity Check:**
    - Verify ground and power connections.

### Using an Oscilloscope

1. **Signal Integrity Test:**
    - Probe RF_P/N while transmitting to ensure proper RF output.
2. **Digital Signal Check:**
    - Monitor UART TX/RX lines for clean data transitions.

### Using a Spectrum Analyzer

1. **RF Signal Test:**
    - Measure frequency and power of RF output to confirm proper transmission.
2. **Interference Analysis:**
    - Check for unexpected harmonics or noise in the RF spectrum.

## Usage Notes

- Use a proper impedance-matched antenna for optimal wireless performance.
- Ensure low-ESR capacitors are used on the power supply lines.
- Handle with ESD-safe equipment to avoid damage.

## Practical Application Guide

### Recommended Circuit Configuration

- **Power Supply:** Use a 3.3 V regulator with sufficient current capacity.
- **Antenna Matching:** Follow reference design for antenna impedance matching.
- **Debugging Interface:** Use SWD lines for firmware programming.

### Troubleshooting Tips

- If no RF output, verify antenna connection and software settings.
- For communication issues, check UART settings and crystal accuracy.
- Monitor power consumption to identify potential sleep mode issues.

### Safety Considerations

- Avoid transmitting without a proper antenna connected.
- Ensure proper thermal dissipation for extended transmissions.
- Follow regulatory requirements for RF emissions.

## Advanced Tips & Insights

- **Antenna Selection:** Choose a high-gain antenna for maximum range.
- **Frequency Calibration:** Regularly calibrate the frequency reference for accurate RF performance.
- **Power Optimization:** Use power profiling tools to identify unnecessary current drains.
- **Network Testing:** Test in realistic environments to account for interference and signal attenuation.

## Inventory Integration Plan

**RFID Tag ID:** TBD **Location:** Component Shelf - Wireless MCUs

**Markdown Code:** `#cc2652p1frgzr`

Scan with RFID scanner to pull up this document when needed.