# 🎭 FaceID — Campus Biometric Access Control System

A fully browser-based face recognition system built with vanilla JavaScript and TensorFlow.js. No backend, no server, no installation — just open the HTML file and it works.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Visit%20Site-00e5ff?style=for-the-badge&logo=netlify)](https://your-link-here.netlify.app)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow?style=for-the-badge&logo=javascript)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

---

## 📸 Demo

> Register a face → Select a mode → Scan → Get instant result

The system runs entirely in the browser using your device's camera. All face data stays on your device — nothing is sent to any server.

---

## ✨ Features

- **Face Registration** — Enroll any number of people directly through the browser camera. Add multiple samples per person for higher accuracy.
- **Attendance Marking** — Recognize and log attendance for classes or sessions.
- **Campus Gate Entry/Exit** — Auto-detects whether the next scan is an entry or exit per person and logs it with a timestamp.
- **Library Access** — Face-based identity verification for library entry.
- **Activity Records** — View complete history per roll number — all gate entries, exits, attendance, and library events in one place, filterable by module.
- **Confidence Score** — Every recognition result shows a match confidence percentage.
- **100% Client-Side** — No backend, no database, no API keys needed.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **HTML / CSS / JavaScript** | Frontend — single file, zero dependencies |
| **face-api.js** | Face detection, landmark extraction, and recognition |
| **TensorFlow.js** | Underlying ML runtime for face-api.js |
| **WebRTC (getUserMedia)** | Live camera access in the browser |
| **Canvas API** | Real-time face bounding box overlay |

The face recognition uses a **128-dimensional face embedding** model (similar to FaceNet). Matching is done via **Euclidean distance** with a tuned threshold — no training required.

---

## 🚀 Getting Started

### Option 1 — Just open the file
```bash
# Clone the repo
git clone https://github.com/ankit637836/Biometric-Access-for-College.git

# Open in browser
open index.html
```
No `npm install`, no build step. Works as a plain HTML file.

### Option 2 — Serve locally (recommended to avoid camera permission issues)
```bash
# Using Python
python -m http.server 8000

# Or using Node.js
npx serve .
```
Then visit `http://localhost:8000`

---

## 📖 How to Use

### 1. Register Faces (Admin Panel)
- Click **"⚙ ADMIN — Register Faces"** on the home screen
- Enter the person's **Name**, **Roll/ID Number**, and **Role**
- Click **"Capture & Register"** while facing the camera
- Add **3–5 samples** per person (different angles) for best accuracy

### 2. Mark Attendance
- Select **"Mark Attendance"** from the home screen
- Face the camera and click **"Scan Face"**
- The system identifies the person and logs the timestamp

### 3. Campus Gate (Entry / Exit)
- Select **"Campus Gate"** — entry and exit are tracked in the same flow
- The system **auto-toggles** between Entry and Exit for each person based on their last recorded action
- All gate crossings are stored with date and time

### 4. View Records
- Click **"View Records"** from the home screen
- Browse logs grouped by roll number
- Filter by **Gate / Attendance / Library** or search by name

---

## 📁 Project Structure

```
face-recognition-system/
│
├── index.html          # Entire application (self-contained)
└── README.md           # This file
```

Everything — HTML, CSS, and JavaScript — lives in a single `index.html` file. The ML models are loaded at runtime from a public CDN.

---

## ⚙️ How the Recognition Works

```
Camera Frame
     │
     ▼
TinyFaceDetector        ← Finds face bounding box
     │
     ▼
FaceLandmark68Net       ← Maps 68 facial landmarks
     │
     ▼
FaceRecognitionNet      ← Generates 128-float descriptor vector
     │
     ▼
Euclidean Distance      ← Compared against all registered descriptors
     │
     ▼
Threshold Check (0.52)  ← Match if distance < threshold
     │
     ▼
Identity / Unknown
```

---

## 🔒 Privacy

- All face data (embeddings) is stored **in-memory** only — it is never uploaded, never persisted to disk, and disappears when you close the tab.
- The camera feed is processed locally using WebRTC.
- No analytics, no tracking, no external API calls (except loading the ML model weights from a CDN on first load).

---

## 🔮 Planned Features

- [ ] Export attendance/records to CSV
- [ ] Persistent storage using IndexedDB (data survives page refresh)
- [ ] Admin password protection
- [ ] Class/session management
- [ ] Multi-camera support
- [ ] Dark/light theme toggle
- [ ] QR code backup of registered face data

---

## 🐛 Known Limitations

- Face data is lost on page refresh (in-memory only — see roadmap above)
- Recognition accuracy depends on lighting conditions — natural front-facing light works best
- ML models (~6 MB) are loaded from CDN on first visit, so an internet connection is required
- Works best on Chrome and Edge; Firefox may have minor WebRTC differences

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙋 Author

**Your Name**
- GitHub: [https://github.com/ankit637836/](https://github.com/ankit637836/)
- LinkedIn: [https://www.linkedin.com/in/ankit-80062b1b9/](https://www.linkedin.com/in/ankit-80062b1b9/)

---

> Built as a demonstration of browser-native machine learning using WebRTC and TensorFlow.js — no cloud services or server infrastructure required.
