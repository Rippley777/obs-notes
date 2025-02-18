	


|Component|What It Does|How To Think About It|
|---|---|---|
|**Resistor**|Limits current|Like a water pipe with a narrower section—it restricts flow.|
|**Capacitor**|Stores & releases energy|Like a tiny battery, but it charges/discharges **way faster**.|
|**Inductor**|Resists changes in current|Imagine a car trying to stop suddenly—it resists sudden changes in speed.|
|**Transistor**|Acts as a switch or amplifier|Like an electronic faucet—small input controls a **big** output.|

- **Electricity is like water flow** (DC analogy)
    
    - **Voltage (V)** = Water pressure (force pushing water through a pipe)
    - **Current (I)** = Water flow rate (amount of water moving through the pipe)
    - **Resistance (R)** = Narrowness of the pipe (how much it restricts flow)
- **Basic Circuit Components & Their Role in the Flow**
    
    - **Resistor (R)** → Resists current, limiting flow like a smaller pipe.
    - **Capacitor (C)** → Stores and releases energy like a bucket collecting water and dumping it out.
    - **Inductor (L)** → Acts like a spring, resisting changes in current, storing energy in a magnetic field.
    - **Transistor (Q)** → Acts as a valve or switch, controlling the flow of current (via voltage or current input).
- **More on Each Component**
    
    - **Resistor:** Reduces current flow, dissipating energy as heat (Ohm’s Law: V=IRV = IRV=IR).
    - **Capacitor:** Stores electrical charge and releases it when needed. Blocks DC but passes AC.
    - **Inductor:** Creates a magnetic field when current flows. Resists changes in current (like a flywheel resisting changes in motion).
    - **Transistor:** A switch or amplifier. Can turn current on/off (digital logic) or amplify signals (analog circuits).


## Current
**Current** is measured in **amperes (A)**, or **amps** for short.

### Here’s how it all connects:

- **Voltage (V)** is measured in **volts** (V) → The "pressure" pushing electrons.
- **Current (I)** is measured in **amperes (A)** → The "flow" of electrons.
- **Resistance (R)** is measured in **ohms (Ω)** → The "restriction" to the flow.

### Ohm’s Law ties it all together:
![[ohms_law_equation.png]]


- If you increase **voltage**, more current flows (if resistance stays the same).
- If you increase **resistance**, less current flows (if voltage stays the same).

For example:

- A 12V battery connected to a **6Ω resistor** will produce **2A of current** (since 12V/6Ω=2A12V / 6Ω = 2A12V/6Ω=2A).
- If the resistor were **3Ω**, the current would double to **4A** (12V/3Ω=4A12V / 3Ω = 4A12V/3Ω=4A).


# Transistors
## Mosfets
A **MOSFET** (_Metal-Oxide-Semiconductor Field-Effect Transistor_) is a **fancy transistor**, specifically a type of **field-effect transistor (FET)** that is widely used in power electronics and digital circuits.

### How It Differs from a Regular Transistor (BJT)

- **BJT (Bipolar Junction Transistor):** Controlled by _current_.
- **MOSFET:** Controlled by _voltage_.

### Why MOSFETs Are Fancy:

- **More efficient**: Requires almost no input current to switch on/off.
- **Faster switching**: Ideal for high-speed and high-power applications.
- **Less heat**: Because of lower resistance when turned on (low RDS(on)R_{DS(on)}RDS(on)​).

### How It Works:

- A MOSFET has **three terminals**:
    1. **Gate (G):** Controls the flow of current.
    2. **Drain (D):** Where current enters.
    3. **Source (S):** Where current exits.
- Applying a voltage to the **gate** opens or closes the "valve" between **drain** and **source**.

### Two Main Types:

- **N-channel MOSFET:** Turns on when gate voltage is **positive** relative to the source. (More common)
- **P-channel MOSFET:** Turns on when gate voltage is **negative** relative to the source.

### When to Use a MOSFET:

- Power supplies
- Motor drivers
- Amplifiers
- Switching circuits (like an Arduino controlling a motor)

It’s basically a **superior switch** compared to a regular transistor when it comes to efficiency and speed.