- **SCK** (Serial Clock)
- **MISO** (Master In Slave Out)
- **MOSI** (Master Out Slave In)
- **SS** (Slave Select / Chip Select)
- **VCC** (Power)
- **GND** (Ground)
- **RQ** (Request or Interrupt)
- **RSTO** (Reset)

This is likely an **MFRC522** or a similar SPI-based RFID reader module.

---

### **Wiring Instructions for Arduino (SPI Mode)**

|**RFID Pin**|**Arduino Pin (Uno)**|**Description**|
|---|---|---|
|**VCC**|**3.3V**|Power (do NOT use 5V)|
|**GND**|**GND**|Ground|
|**SCK**|**D13**|SPI Clock|
|**MOSI**|**D11**|SPI Data (Master Out)|
|**MISO**|**D12**|SPI Data (Master In)|
|**SS**|**D10**|Slave Select (Chip Select)|
|**RSTO**|**D9**|Reset|

**Important:**

- **Use 3.3V for power**, as many RFID modules aren't 5V-tolerant.
- The **RQ** pin is usually optional unless you need an interrupt-driven approach.

---

### **Arduino Code (MFRC522 Example)**

Make sure to install the **MFRC522** library if this is an **MFRC522** RFID module.

1. **Install Library:**  
    Go to **Tools → Manage Libraries** and search for **MFRC522**. Install it.
    
2. **Upload this Code:**
    

```cpp
#include <SPI.h>
#include <MFRC522.h>

#define SS_PIN 10
#define RST_PIN 9

MFRC522 mfrc522(SS_PIN, RST_PIN); // Create MFRC522 instance.

void setup() {
  Serial.begin(9600);
  SPI.begin();         // Initiate SPI bus
  mfrc522.PCD_Init();  // Initiate MFRC522
  
  Serial.println("RFID Reader Ready. Scan a tag...");
}

void loop() {
  // Look for new RFID cards
  if (!mfrc522.PICC_IsNewCardPresent()) {
    return;
  }

  // Select one of the RFID cards
  if (!mfrc522.PICC_ReadCardSerial()) {
    return;
  }

  // Print card UID
  Serial.print("UID tag: ");
  for (byte i = 0; i < mfrc522.uid.size; i++) {
    Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? "0" : "");
    Serial.print(mfrc522.uid.uidByte[i], HEX);
    Serial.print(" ");
  }
  Serial.println();

  delay(1000);
}

```

---

### **How It Works**

1. **Power the module** with 3.3V.
2. **Open Serial Monitor** (9600 baud) in Arduino IDE.
3. **Scan an RFID tag** near the reader.
4. It should print the **UID (Unique ID)** of the card.

---

### **Troubleshooting**

- If no cards are detected, double-check **wiring**.
- Ensure the **Arduino IDE Serial Monitor** is set to **9600 baud**.
- Make sure to use **3.3V** power, as many RFID modules are sensitive to higher voltages.