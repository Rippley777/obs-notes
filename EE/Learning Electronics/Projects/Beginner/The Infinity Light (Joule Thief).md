### ⚡️ **The Infinity Light (Joule Thief)** ⚡️

A **Joule Thief** circuit makes you feel like you’ve discovered free energy because it can light an LED from a "dead" AA battery (like, down to **0.5V**) when it normally needs **2-3V**.

**You'll feel like:**  
🧙‍♂️ _"Behold! I summon photons from the void!"_

---

### 🔧 **Parts You Need:**

- 1x **"Dead" AA battery** (anything below 1.0V is perfect)
- 1x **LED** (any color—green or blue is even more impressive)
- 1x **NPN transistor** (e.g., 2N3904, BC547)
- 1x **Toroidal inductor or any ferrite core** (you can also wrap wire around a screw if you’re feeling rogue)
- 1x **Resistor** (1kΩ)
- **Magnet wire** (your new obsession)

---

### 🛠️ **How It Works (Magic in 3 Steps)**

1. The inductor and transistor form a feedback loop.
2. The coil builds up magnetic energy and then releases it as a **high-voltage spike**.
3. That spike **boosts the voltage** enough to power the LED, even from a dead battery.

---

### ⚙️ **Wiring Guide**

plaintext

CopyEdit

            `[AA Battery +]                    │               [1kΩ Resistor]                   │                   │────[Base of NPN]                   │      Coil (primary)────┐                   │    │  [Collector]──────┘    │────[LED]────[Battery -]             (NPN)       Coil (secondary)`

- Wrap the coil with **two strands of magnet wire** (~10 turns around a pen or screw).
- Leave one end of each strand as the **primary** and **secondary** coil leads.
- The transistor will **oscillate** the current through the coil, creating high-voltage pulses.

---

### 🚨 **What You’ll See:**

- That "dead" battery will suddenly light the LED like it’s fresh out of the pack.
- The inductor whines faintly (high-frequency oscillation).
- You'll sit back, grin like a mad scientist, and wonder why the power grid even exists.

---

### 🤯 **Why It Feels Like Magic:**

- You took a battery destined for the trash and wrung **light** out of it.
- You just built a **self-oscillating, high-voltage boost converter**.
- If you increase the turns and get clever with the coil, you can push more power through and maybe even light **multiple LEDs** in series.

---

### 🌐 **Next-Level Flex:**

- Try different core materials: ferrite beads, screws, bolts—see what works best.
- Use your **BladeRF** to check the oscillation frequency (it’s usually in the 30–100kHz range).
- Wrap more turns on the coil and see if you can power something bigger.
- Record a video and caption it: **“I made light from a dead battery. Fear me.”** 💥⚡️

---

Let me know how it goes! And remember: if the LED doesn’t light, **reverse it**.