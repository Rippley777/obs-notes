### **🔥 Baby’s First AVP App (TypeScript Edition)**

Ahh, I feel you on Python's dev experience—it’s kinda janky sometimes. Let's do this **the TypeScript way** for **better DX** and **easier debugging**.

---

## **🛠 Step 1: Setup the Project**

We're using:

- `ffmpeg` (for video/audio conversion 🔄)
- `fluent-ffmpeg` (FFmpeg wrapper for Node.js)
- `node-record-lpcm16` (to record audio 🎤)
- `opencv4nodejs` (for webcam stuff 📷)

### **📌 Install Dependencies**

First, set up a new project


```bash
mkdir baby-avp-ts && cd baby-avp-ts
yarn init -y

```

Then install the packages:


```bash
yarn add fluent-ffmpeg node-record-lpcm16
yarn add -D @types/node typescript ts-node

```

**For OpenCV (optional, for video capture):**

- Install OpenCV on **Mac/Linux**:
```bash
brew install opencv

```

Install OpenCV on **Windows**:


```bash
choco install opencv

```


Then install the bindings:


```bash
yarn add opencv4nodejs

```
## **🎥 Step 2: Open the Webcam**

Let's **capture video from the webcam** using `opencv4nodejs`.

📌 **Run this script**

```ts
import cv from 'opencv4nodejs';

const webcam = new cv.VideoCapture(0);

setInterval(() => {
  const frame = webcam.read();
  cv.imshow('Baby’s First AVP (TypeScript)', frame);
  cv.waitKey(1);
}, 33); // ~30 FPS

```

🎉 **What happens?**

- Your webcam **opens**.
- You see your **live feed** in a window.
- **Close it** by clicking the ❌ button.

If OpenCV **complains**, try `yarn add -D @types/opencv4nodejs`.

---

## **🎤 Step 3: Record Audio**

Let's **record a short audio clip**.

📌 **Run this script**

```tsx
import record from 'node-record-lpcm16';
import fs from 'fs';

const outputFile = 'baby_first_audio.wav';
const fileStream = fs.createWriteStream(outputFile);

console.log('🎤 Recording for 5 seconds...');
const rec = record.start({
  sampleRate: 44100,
  channels: 1,
  audioType: 'wav',
});

setTimeout(() => {
  record.stop();
  fileStream.end();
  console.log(`✅ Saved to ${outputFile}`);
}, 5000);

rec.pipe(fileStream);

```

🎉 **What happens?**

- It records **5 seconds** of your voice.
- Saves it as **`baby_first_audio.wav`**.
- Play it using `open baby_first_audio.wav` (Mac/Linux) or just double-click it on Windows.

---

## **🔄 Step 4: Convert Files (FFmpeg)**

We’ll use **FFmpeg** for **conversions**.

📌 **Convert WAV to MP3**

```tsx
import ffmpeg from 'fluent-ffmpeg';

ffmpeg('baby_first_audio.wav')
  .output('baby_first_audio.mp3')
  .on('end', () => console.log('✅ Converted to MP3'))
  .run();

```

📌 **Convert Video to Grayscale:**

```tsx
ffmpeg('input.mp4')
  .output('gray_output.mp4')
  .videoFilters('format=gray')
  .on('end', () => console.log('✅ Video converted to grayscale'))
  .run();

```

🎉 **What happens?**

- The **audio converts to MP3**.
- The **video converts to grayscale**.

---

## **🚀 What’s Next?**

✅ **Webcam works**  
✅ **Audio recording works**  
✅ **FFmpeg conversions work**

Now, do you wanna:

1. **Record video with audio at the same time?**
2. **Add filters/effects to the video?**
3. **Make a simple media player in Electron?**
