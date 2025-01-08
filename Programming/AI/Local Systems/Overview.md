### **1. Core Concept: Make the Machines Talk**

You’ll use one machine as your "main driver" (boss machine) and connect others to it. Together, they’ll act like one big brain for running AI.

---

### **2. What You’re Working With**

- **GPU (Graphics Card)**: This is the heavy lifter. Your AI does math—**a LOT of math**—and GPUs are math powerhouses.
    - Your **3070** is the superhero, and the **1080 Ti** is the trusty sidekick.
- **CPU (Processor)**: Think of this as the manager, keeping the operation running smoothly.
    - The **i7-8086K** is your best manager. Use it in the main machine.
- **Memory (RAM)**: Helps your AI keep stuff in its short-term memory.
- **Storage (HDD/SSD)**: Where you keep your programs and data.

---

### **3. Wiring It All Up**

Here’s how to build the setup:

#### **A. Pick Your Main Machine**

- Use the one with the **3070 GPU** and **i7-8086K CPU**. It’s the fastest combo.
- Add **16GB+ of RAM** if you have it—AI loves memory.
- Use an SSD for quick access to data (even a small one for your operating system).

#### **B. Set Up the Sidekicks**

- Use the other machines as "helpers" for extra computing power.
- You can link them together over your **local network** (your home Wi-Fi or, better yet, Ethernet cables).

#### **C. Networking Magic**

- **Ethernet cables**: Plug each machine into the same router/switch for faster communication.
- Install software like **NVIDIA CUDA + NCCL** to let the GPUs share workloads.

---

### **4. Install the Brains (Software)**

Here’s the essential software stack:

1. **Operating System (OS):**
    
    - Use **Linux** (Ubuntu is beginner-friendly and free!) for better AI performance.
    - Install drivers for your GPUs (NVIDIA drivers).
2. **AI Frameworks (The Tools):**
    
    - Install **Python** (the language of AI).
    - Set up **PyTorch** or **TensorFlow** (libraries for running AI).
    - Install NVIDIA’s **CUDA Toolkit** (teaches your GPUs to do AI math).
3. **Orchestrator Software (Optional):**
    
    - Use **Docker** for clean, isolated environments.
    - Try **Ray** or **Dask** to manage tasks across multiple machines.

---

### **5. Power On and Test**

- Power up all machines.
- On your main machine, install a small AI model (e.g., GPT-like or Stable Diffusion).
- Run a test workload to see the GPUs in action.

---

### **6. Bonus Tips**

- Use **SSH** (remote control software) to command helper machines from the main one.
- For fun experiments, try tools like **Runpod** or **FastAPI** to serve your AI locally.