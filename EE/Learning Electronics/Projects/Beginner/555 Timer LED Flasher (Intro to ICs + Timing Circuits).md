**Goal:** Use an integrated circuit (IC) to create a stable, adjustable blinking light.

#### 🧩 **How It Works:**

- The 555 timer IC generates a square wave signal.
- The LED blinks with timing determined by resistor-capacitor combinations.

**🛠️ Components:**

- 1x **555 Timer IC**
- 2x Resistors (e.g., 10kΩ and 100kΩ)
- 1x Capacitor (10µF)
- 1x LED
- 1x Power source (5–9V)

**🔌 Wiring (Astable Mode):**

- Pin 1: GND
- Pin 2: Trigger → Connect to Pin 6 (Threshold)
- Pin 3: Output → LED (through a resistor)
- Pin 4: Reset → VCC
- Pin 5: Control → Ground via 0.01µF cap
- Pin 6: Threshold → Connect to Pin 2
- Pin 7: Discharge → Connect to resistor network
- Pin 8: VCC

💡 **What You Learn:**

- How **timing circuits** work.
- Basics of **integrated circuits (ICs)**.
- The magic of PWM (Pulse Width Modulation) for brightness control.
