**Goal:** Use a transistor to control a DC motor, understanding amplification and switching.

#### 🧩 **How It Works:**

- A transistor acts like a switch—when the base receives a signal, it powers the motor.
- Add a **diode** to protect the circuit from voltage spikes (motors generate back-EMF).

**🛠️ Components:**

- 1x **NPN Transistor** (e.g., 2N2222)
- 1x **Motor** (small DC motor)
- 1x **Diode** (e.g., 1N4007)
- 1x **Resistor** (1kΩ for transistor base)
- 1x Power source (5–12V)

**🔌 Wiring:**

- Power → Motor → Collector of transistor → Emitter to ground.
- Base gets signal through a resistor.
- **Diode** goes across the motor terminals in reverse (cathode to VCC).

💡 **What You Learn:**

- **Transistor basics** (NPN operation).
- **Inductive loads** and the importance of **flyback diodes**.
- **PWM control** for speed adjustment.