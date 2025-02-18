### 📚 **Inductors: The Basics**

Inductors are like the **momentum hoarders** of the electronics world. They resist _changes in current_ the same way a flywheel resists sudden changes in speed. Here’s the simple breakdown:

1. **Magnetic Fields & Current:**
    
    - When current flows through a coil of wire, it generates a magnetic field.
    - More current = stronger field.
2. **Inductive Reactance (Resistance to Change):**
    
    - If you try to _increase_ current suddenly, the magnetic field resists the change by inducing a voltage **opposing the current's rise**.
    - If you try to _decrease_ current, the collapsing magnetic field induces a voltage to **keep the current flowing**.
    - **Key Equation:** 
	    ![[resistance_to_change_equation.png]]
	    — the voltage across an inductor is proportional to how fast the current changes.
3. **Practical Impact:**
    
    - In **DC circuits**, inductors act like **wires** after the magnetic field stabilizes.
    - In **AC circuits**, inductors **oppose higher frequencies**.
        - That’s why inductors are common in **low-pass filters**: they let the low-frequency signals pass but block the high-frequency noise.
4. **Wireless Energy Relevance:**
    
    - **Tesla Coils** = tuned LC circuits (inductor + capacitor) at resonance.
    - The **inductive field** is what you’re trying to “throw” across space to transmit energy.