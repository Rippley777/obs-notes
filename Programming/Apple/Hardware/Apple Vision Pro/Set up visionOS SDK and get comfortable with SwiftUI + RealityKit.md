To set up the **visionOS SDK** and get comfortable with **SwiftUI + RealityKit**, you’ll need to do the following:

---

## **1. Install Xcode 15+ and visionOS SDK**

Since AVP runs **visionOS**, you’ll need the latest **Xcode** version with the **visionOS SDK**.

### **Step 1: Get Xcode 15+**

🔹 Open the **Mac App Store** and install **Xcode** if you haven’t already.  
🔹 If you need the latest beta:

- Go to [Apple’s Developer site](https://developer.apple.com/download/)
- Download and install the **latest Xcode beta**.

### **Step 2: Install visionOS SDK**

1. Open **Xcode** → Go to **Settings** → **Platforms**.
2. Click the **+** button and add **visionOS SDK**.

---

## **2. Create a visionOS App Project**

Once the SDK is installed, you can create a **new project** with **visionOS support**.

### **Step 1: Start a New Project**

1. Open **Xcode**.
2. Click **Create a new Xcode project**.
3. Select **visionOS App** (SwiftUI-based).
4. Name your project (e.g., `AVP_Test`).
5. Set **Interface** to **SwiftUI**.
6. Set **Language** to **Swift**.

### **Step 2: Run in the Simulator**

1. Connect your **AVP Developer Strap** (if available).
2. Choose a **visionOS Simulator**:
    - Click **the device selector** in Xcode.
    - Choose **Apple Vision Pro (Simulator)**.
3. Click **Run** (▶) to test the app.

---

## **3. Learn the Basics of SwiftUI + RealityKit**

Now that you have a visionOS app, let’s break down **SwiftUI** and **RealityKit**:

### **Basic SwiftUI UI for visionOS**

SwiftUI is the main UI framework. Here’s a **simple SwiftUI view** for visionOS

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, visionOS!")
                .font(.largeTitle)
                .padding()

            Button("Tap Me") {
                print("Button tapped!")
            }
            .padding()
            .background(.blue)
            .foregroundColor(.white)
            .clipShape(RoundedRectangle(cornerRadius: 10))
        }
    }
}

#Preview {
    ContentView()
}

```

#### **What’s happening here?**

- **`VStack`** stacks elements vertically.
- **`Text`** displays text.
- **`Button`** prints to the console when tapped.
- **`#Preview`** enables live previews in Xcode.

---

### **Basic RealityKit 3D Object in visionOS**

RealityKit handles **3D objects and spatial elements**.

#### **Step 1: Create a RealityView**

Replace your `ContentView.swift` with this

```swift
import SwiftUI
import RealityKit

struct ContentView: View {
    var body: some View {
        RealityView { content in
            let sphere = ModelEntity(mesh: .generateSphere(radius: 0.1))
            sphere.components.set(InputTargetComponent())
            content.add(sphere)
        }
        .gesture(
            TapGesture().targetedToAnyEntity().onEnded { event in
                print("Sphere tapped!")
            }
        )
    }
}

#Preview {
    ContentView()
}

```

#### **What’s happening here?**

- **`RealityView`** loads 3D objects into visionOS.
- **`ModelEntity`** creates a **3D sphere**.
- **`TapGesture()`** lets you interact with objects.

✅ **Try running this in the AVP simulator!**  
🔹 You should see a **floating sphere** that you can **tap**.

---

## **4. Experiment with Spatial UI**

You can create **floating UI elements** that aren’t confined to a window.

### **Example: Floating UI Panel**

```swift
import SwiftUI
import RealityKit

struct ContentView: View {
    var body: some View {
        RealityView { content in
            let box = ModelEntity(mesh: .generateBox(size: 0.2))
            box.position = SIMD3(0, 0, -1) // Places box 1 meter in front
            content.add(box)
        }
    }
}

#Preview {
    ContentView()
}

```

🔹 The **box appears 1 meter in front of you** in space.

---

## **5. Deploy to Apple Vision Pro**

If you have an **AVP Developer Strap**, you can test on real hardware:

1. **Enable Developer Mode** on AVP:
    - Open **Settings** → **Privacy & Security** → **Developer Mode**.
    - Toggle **ON** and restart.
2. **Pair AVP with Xcode**:
    - Connect AVP via **Wi-Fi** or USB-C.
    - Open Xcode → **Window** → **Devices & Simulators**.
    - Select your AVP and click **Pair**.
3. **Deploy Your App**:
    - In Xcode, select **your AVP** from the **device list**.
    - Click **Run** (▶) to install and launch the app on AVP.

---

## **Next Steps**

4. **Modify the RealityKit example**:
    - Change the **object shape** (box, sphere, plane).
    - Add a **gesture interaction** (pinch to scale, rotate, etc.).
5. **Try Spatial UI**:
    - Create a **floating menu** that follows your gaze.
6. **Experiment with Vision Pro Sensors**:
    - Play with **hand tracking and object recognition**.
    - Pull in **real-world environment data**.


