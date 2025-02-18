# **Baby’s First AVP App WITH CUSTOM CODE**

We will: 1️⃣ **Open the webcam**  
2️⃣ **Modify video frames (e.g., flip the image, add text, distort)**  
3️⃣ **Record audio and modify samples (e.g., invert, change volume)**  
4️⃣ **Run it inside AVP processing**

---

## **🎥 Modify Video Frames (Live)**

**Goal:** Instead of just showing raw webcam footage, let's **flip it, draw text, and distort pixels.**

📌 **Put this in `video_custom.js`**


```javascript
const cv = require('opencv4nodejs');

const webcam = new cv.VideoCapture(0);

setInterval(() => {
  let frame = webcam.read();

  // 🔄 Flip video horizontally
  frame = frame.flip(1);

  // 📝 Draw text on the video
  frame.putText('HELLO AVP WORLD', new cv.Point(50, 50), cv.FONT_HERSHEY_SIMPLEX, 1, new cv.Vec(255, 255, 255), 2);

  // 🤪 Mess with pixels (distort)
  frame.getDataAsArray().forEach((row, y) => {
    row.forEach((pixel, x) => {
      if (x % 20 === 0) { // Every 20 pixels, change color
        frame.set(y, x, [0, 255, 0]); // Make it green
      }
    });
  });

  cv.imshow('Baby AVP with Custom Code', frame);
  cv.waitKey(1);
}, 33); // ~30 FPS

```

🎉 **What happens?**

- **Flips the webcam video** like a mirror
- **Adds a "HELLO AVP WORLD" text overlay**
- **Randomly changes pixel colors for fun distortion**
- Runs **inside the AVP pipeline!**

**Run it:**



```bash
node video_custom.js

```


🔥 **Now your code is inside AVP!** 🎥🚀

---

## **🎤 Modify Audio (Live)**

**Goal:** Instead of just recording audio, let’s **invert samples, mess with volume, and distort audio.**

📌 **Put this in `audio_custom.js`**


```javascript
const record = require('node-record-lpcm16');
const fs = require('fs');

console.log('🎤 Recording & Modifying Audio for 5 seconds...');
const file = fs.createWriteStream('baby_audio.raw');

const stream = record.start({
  sampleRate: 44100,
  channels: 1,
}).on('data', (chunk) => {
  // 🔄 Invert samples (simple effect)
  const buffer = Buffer.from(chunk);
  for (let i = 0; i < buffer.length; i++) {
    buffer[i] = 255 - buffer[i]; // Invert the sample
  }
  file.write(buffer);
});

setTimeout(() => {
  record.stop();
  console.log('✅ Audio recorded with modifications');
}, 5000);

```

🎉 **What happens?**

- **Records audio but inverts the samples** (sound might be creepy)
- **Saves the modified audio**

**Run it:**



```bash
node audio_custom.js
ffplay -f s16le -ar 44100 -ac 1 -i baby_audio.raw

```

🔥 **Now your audio modifications are inside the AVP pipeline!** 🎤🚀

---

## **🔄 Convert Video & Apply Custom Filters**

Now let’s process a **saved** video file and apply a **glitch effect**.

📌 **Put this in `convert_custom.js`**


```javascript
const ffmpeg = require('fluent-ffmpeg');

ffmpeg('input.mp4')
  .videoFilters([
    'eq=brightness=0.06:saturation=2', // Make colors pop
    'hue=s=0', // Remove color
    'noise=alls=50:allf=t' // Add a glitchy noise effect
  ])
  .output('glitch_video.mp4')
  .on('end', () => console.log('✅ Glitchy video created'))
  .run();

```

🎉 **What happens?**

- **Increases brightness**
- **Removes color**
- **Adds a noisy glitch effect**

**Run it:**


```javascript
node convert_custom.js

```

🔥 **Now your code is modifying video inside AVP!** 🎬🚀

---

# **🥇 What We Just Did**

✅ **Modified live webcam video inside the AVP pipeline**  
✅ **Modified live audio before saving**  
✅ **Added a glitch effect to a video file**

---

# **💥 Next Steps**

**Now that you have your code running inside AVP, do you wanna:**  
1️⃣ **Overlay live filters on video (blur, edge detection, emoji tracking)?**  
2️⃣ **Auto-tune or add voice effects to live audio?**  
3️⃣ **Build a simple "deepfake" by swapping faces in the AVP pipeline?**