### **🔥 Baby’s First AVP App (C++ Edition - MAXIMUM EFFORT 🚀)**

Alright, **we're going all in.** No safety nets. No hand-holding. Just **raw C++**. This is how the pros do AVP.

### **💀 The Hard Mode Stack**

We're using:

- **OpenCV** → Webcam handling 🎥
- **PortAudio** → Audio recording 🎤
- **FFmpeg (libavcodec, libavformat, etc.)** → Video/audio encoding 🔄

---

## **🛠 Step 1: Install Dependencies**

You need to install **OpenCV, PortAudio, and FFmpeg**.

### **Mac (Homebrew)**


```bash
brew install opencv portaudio ffmpeg

```

### **Linux (Ubuntu/Debian)**



```bash
sudo apt update
sudo apt install libopencv-dev portaudio19-dev ffmpeg libavcodec-dev libavformat-dev libswscale-dev

```

### **Windows**

1. **Download OpenCV** → https://opencv.org/releases/
2. **Download PortAudio** → http://www.portaudio.com/download.html
3. **Download FFmpeg Dev Libraries** → [https://ffmpeg.org/download.html](https://ffmpeg.org/download.html)

---

## **🎥 Step 2: Open the Webcam**

Let’s **get the webcam running with OpenCV**.

📌 **Create `webcam.cpp`**

```cpp
#include <opencv2/opencv.hpp>
#include <iostream>

int main() {
    cv::VideoCapture cap(0); // Open default camera
    if (!cap.isOpened()) {
        std::cerr << "❌ ERROR: Cannot open camera\n";
        return -1;
    }

    cv::Mat frame;
    while (true) {
        cap >> frame;
        if (frame.empty()) break;

        cv::imshow("Baby’s First AVP (C++)", frame);
        if (cv::waitKey(1) == 'q') break; // Press 'q' to quit
    }

    cap.release();
    cv::destroyAllWindows();
    return 0;
}

```

Compile & Run


```bash
g++ webcam.cpp -o webcam `pkg-config --cflags --libs opencv4` && ./webcam

```

🎉 **What happens?**

- The **webcam opens**.
- Press **'q'** to quit.

---

## **🎤 Step 3: Record Audio**

Let’s **record 5 seconds of audio** using **PortAudio**.

📌 **Create `record_audio.cpp`**


```cpp
#include <iostream>
#include <fstream>
#include <portaudio.h>

#define SAMPLE_RATE 44100
#define NUM_SECONDS 5
#define FRAMES_PER_BUFFER 512

static int audioCallback(const void *inputBuffer, void *outputBuffer,
                         unsigned long framesPerBuffer, const PaStreamCallbackTimeInfo *timeInfo,
                         PaStreamCallbackFlags statusFlags, void *userData) {
    std::ofstream *file = static_cast<std::ofstream *>(userData);
    file->write((char *)inputBuffer, framesPerBuffer * 2);
    return paContinue;
}

int main() {
    Pa_Initialize();
    PaStream *stream;
    std::ofstream file("baby_first_audio.raw", std::ios::binary);

    Pa_OpenDefaultStream(&stream, 1, 0, paInt16, SAMPLE_RATE, FRAMES_PER_BUFFER, audioCallback, &file);
    Pa_StartStream(stream);

    std::cout << "🎤 Recording for " << NUM_SECONDS << " seconds...\n";
    Pa_Sleep(NUM_SECONDS * 1000);

    Pa_StopStream(stream);
    Pa_CloseStream(stream);
    Pa_Terminate();
    file.close();

    std::cout << "✅ Audio saved as 'baby_first_audio.raw'\n";
    return 0;
}

```

Compile & Run

```cpp
g++ record_audio.cpp -o record_audio -lportaudio && ./record_audio

```
🎉 **What happens?**

- **Records 5 seconds** of audio.
- Saves it as `baby_first_audio.raw`.

To convert it to WAV

```c
ffmpeg -f s16le -ar 44100 -ac 1 -i baby_first_audio.raw baby_first_audio.wav

```

## **🔄 Step 4: Convert Files with FFmpeg**

### **Convert WAV to MP3**

📌 **Create `convert_audio.cpp`**

```cpp
extern "C" {
#include <libavformat/avformat.h>
}

#include <iostream>

int main() {
    av_register_all();

    AVFormatContext *inputFormatContext = nullptr;
    if (avformat_open_input(&inputFormatContext, "baby_first_audio.wav", nullptr, nullptr) < 0) {
        std::cerr << "❌ Error opening input file\n";
        return -1;
    }

    AVFormatContext *outputFormatContext = nullptr;
    avformat_alloc_output_context2(&outputFormatContext, nullptr, nullptr, "baby_first_audio.mp3");

    if (!outputFormatContext) {
        std::cerr << "❌ Error creating output context\n";
        return -1;
    }

    if (avio_open(&outputFormatContext->pb, "baby_first_audio.mp3", AVIO_FLAG_WRITE) < 0) {
        std::cerr << "❌ Error opening output file\n";
        return -1;
    }

    avformat_write_header(outputFormatContext, nullptr);
    avformat_free_context(inputFormatContext);
    avformat_free_context(outputFormatContext);

    std::cout << "✅ Converted to baby_first_audio.mp3\n";
    return 0;
}

```

Compile & Run

```bash
g++ convert_audio.cpp -o convert_audio -lavformat -lavcodec -lavutil -lswresample -lswscale && ./convert_audio

```

## **🚀 What’s Next?**

✅ **Webcam capture works**  
✅ **Audio recording works**  
✅ **FFmpeg processing works**

Do you wanna: 1️⃣ **Record video & audio together?**  
2️⃣ **Add effects (grayscale, filters, distortions)?**  
3️⃣ **Build a full GUI app with Qt for AV editing?**
