```
[package]
name = "rust-ar-framework"
version = "0.1.0"
edition = "2021"

[dependencies]
metal = "0.26"      # Metal graphics API
objc = "0.2"        # Interfacing with Swift/Apple APIs
cocoa = "0.24"      # macOS windowing (for debugging on Mac)
gltf = "1.0"        # 3D model loading

[lib]
crate-type = ["cdylib"]  # Allow Swift integration

[[bin]]
name = "ar_app"
path = "src/main.rs"

---

// src/main.rs
use metal::*;
use objc::{msg_send, runtime::Object, class};
use gltf::Gltf;

fn main() {
    // Initialize Metal
    let device = Device::system_default().expect("No Metal device found");
    let queue = device.new_command_queue();
    
    println!("Rust AR Framework Initialized!");
}

#[no_mangle]
pub extern "C" fn start_rust_ar() {
    main();
}

pub fn get_camera_pose() -> [f32; 12] {
    unsafe {
        let ar_class = class!(ARBridge);
        let instance: *mut Object = msg_send![ar_class, new];
        let pose: [f32; 12] = msg_send![instance, getCameraPose];
        pose
    }
}

pub struct Model {
    pub vertices: Vec<f32>,
    pub indices: Vec<u16>,
}

pub fn load_gltf_model(path: &str) -> Model {
    let gltf = Gltf::open(path).unwrap();
    let mut vertices = Vec::new();
    let mut indices = Vec::new();
    
    for scene in gltf.scenes() {
        for node in scene.nodes() {
            if let Some(mesh) = node.mesh() {
                for primitive in mesh.primitives() {
                    let reader = primitive.reader(|_| None);
                    
                    if let Some(vertex_data) = reader.read_positions() {
                        vertices.extend(vertex_data.flat_map(|v| vec![v[0], v[1], v[2]]));
                    }

                    if let Some(index_data) = reader.read_indices() {
                        indices.extend(index_data.into_u16().collect::<Vec<u16>>());
                    }
                }
            }
        }
    }

    Model { vertices, indices }
}

```

```graphql
rust-ar-framework/
│── src/
│   │── main.rs          # Rust entry point
│   │── renderer.rs      # Metal rendering logic
│   │── model_loader.rs  # Load 3D models (glTF)
│   │── bridge.rs        # Rust-Swift bridge (ARKit integration)
│── arkit/
│   │── ARBridge.swift   # Swift ARKit wrapper (Camera, Tracking)
│   │── HandTracking.swift  # Swift Hand Tracking logic
│── shaders/
│   │── shaders.metal    # Metal shaders for rendering
│── Cargo.toml           # Rust dependencies
│── Package.swift        # Swift Package config (optional)
│── README.md            # Documentation

```

## **Step-by-Step File Placement**

### **1️⃣ Rust Code (Inside `src/`)**

- **`main.rs`** → Rust entry point
- **`renderer.rs`** → Handles Metal rendering
- **`model_loader.rs`** → Loads 3D models (glTF, OBJ)
- **`bridge.rs`** → Calls Swift for ARKit data

👉 **Move the Rust files into `src/`**.

---

### **2️⃣ Swift Code for ARKit (Inside `arkit/`)**

- **`ARBridge.swift`** → Handles **camera tracking, ARKit integration**
- **`HandTracking.swift`** → Handles **hand tracking input**

👉 **Move the Swift files into `arkit/` and link them in Xcode**.

---

### **3️⃣ Metal Shaders (Inside `shaders/`)**

- **`shaders.metal`** → Metal vertex and fragment shaders for **3D rendering**

👉 **Move `shaders.metal` into `shaders/`**.

---

## **Building the Framework**

### **1️⃣ Build the Rust Library**



```bash
cargo build --release --target aarch64-apple-darwin

```
This generates `librust_ar_framework.dylib` in `target/release/`, which must be linked in Xcode.

### **2️⃣ Link Rust in Xcode**

- Open **Xcode**.
- Add `librust_ar_framework.dylib` under **"Link Binary with Libraries"**.
- Call Rust from Swift using
```swift
MetalRenderer().startRendering()

```

## **Next Steps**

✅ **Rust + Metal Rendering**  
✅ **ARKit Camera Tracking**  
✅ **Hand Tracking in AR**
