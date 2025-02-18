### 🔧 **How to Put a Fuse In-Line (a.k.a. Inline Fuse Wiring)**

#### **1️⃣ Identify Where the Fuse Goes**

- A fuse is always placed **in series** with the **positive (VCC) line**.
- **Why?** Because you want the fuse to "break the circuit" if too much current flows through.

💡 **Golden Rule:** Power flows through the fuse _before_ it reaches the sensitive component.

---

#### **2️⃣ Cut the Wire (the "Inline" part)**

- Identify the **wire feeding your component**.
- **Cut** the wire at the point where you want to insert the fuse.
- Strip about **1/4" to 1/2"** of insulation from both cut ends.

---

#### **3️⃣ Insert the Fuse**

Now you have two options:

### **Option A: Soldered Inline Fuse (Classic Method)**

- Take the two bare ends of the wire and solder them to the leads of the fuse.
- Use **heat-shrink tubing** to cover and insulate the exposed connections.
- Done! Easy, clean, permanent.

### **Option B: Inline Fuse Holder (Pro Method)**

- Use an **inline fuse holder**—these are plastic holders with wires coming out of both sides.
- Connect each end of the cut wire to the fuse holder leads.
- Insert the fuse into the holder, snap it shut.
- **Pros:** Easy fuse replacement.
- **Look for:** "Automotive inline fuse holders" or "PTC fuse holders" on Digi-Key.

---

#### **4️⃣ Test It**

- Power the circuit and test it under normal load conditions.
- If the fuse blows immediately, double-check for shorts or incorrect ratings.
- If it runs smoothly—congrats, you’re in business!

---

### 🧠 **Pro Tips for Fuse Placement:**

- Always fuse the **positive** line unless you're dealing with ground-referenced designs like automotive circuits.
- **PTC fuses (polyfuses)** can go directly in series with sensitive components like IC power pins.
- For high-current lines, consider a fuse holder rated for the expected amps.

---

### 🛠️ **DIY Tesla Coil Example:**

- Power source → **Fuse** → Primary coil driver circuit → Primary coil.
- If the coil driver tries to pull too much current, the fuse trips before your transistors get crispy.