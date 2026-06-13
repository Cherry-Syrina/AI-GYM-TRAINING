# 🏋️‍♂️ AI Real-Time GYM Trainer

A real-time AI-powered fitness coaching app built with **Streamlit**, **MediaPipe Pose Landmarker**, and **Groq LLM**. The app tracks your exercise form live through your webcam, counts reps, analyzes posture, and gives spoken feedback like a personal trainer.

## ✨ Features

- **Real-time Pose Detection** — Uses MediaPipe Pose Landmarker for accurate body tracking via webcam (powered by `streamlit-webrtc`)
- **Multiple Exercises Supported**
  - Squats
  - Push-ups
  - Biceps Curls (Dumbbell)
  - Shoulder Press
  - Lunges
- **Form Analysis & Rep Counting** — Each exercise has a dedicated detector that calculates joint angles, tracks depth/range of motion, and flags posture issues
- **AI Voice Coach** — Groq-powered LLM (`llama-3.3-70b-versatile`) gives contextual feedback on your form, converted to speech via gTTS
- **Session Tracking & History** — User login system with SQLite-backed exercise history (`data.db`)
- **Custom UI** — Styled with a custom theme and font (AdobeClean)

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Frontend / App | Streamlit |
| Pose Detection | MediaPipe Tasks (Pose Landmarker) |
| Video Streaming | streamlit-webrtc |
| AI Coaching | Groq API (LLaMA 3.3 70B) |
| Text-to-Speech | gTTS |
| Database | SQLite |
| Computer Vision | OpenCV |

## 📁 Project Structure

```
AI-GYM-TRAINING/
├── main.py                    # App entry point
├── core/                       # Base exercise class
├── detectors/                  # Exercise-specific form/rep logic
│   ├── squat.py
│   ├── pushup.py
│   ├── biceps_curl.py
│   ├── shoulder_press.py
│   └── lunges.py
├── ml_models/
│   └── pose_landmarker_full.task   # MediaPipe pose model
├── services/
│   ├── auth/                   # Login wall
│   ├── config/                 # Exercise options, pose connections, prompts
│   ├── coaching/                # LLM coach, TTS, voice pipeline
│   ├── persistence/             # SQLite exercise repository
│   ├── state/                   # Session defaults
│   ├── tracking/                # Metrics syncing
│   ├── ui/                       # CSS/font loaders
│   └── vision/                   # Webcam video processor (pose tracking)
├── static/                      # Custom CSS & fonts
└── requirements.txt
```

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Cherry-Syrina/AI-GYM-TRAINING.git
cd AI-GYM-TRAINING
```

### 2. Create a virtual environment

```bash
python -m venv .venv
.venv\Scripts\activate      # Windows
source .venv/bin/activate   # macOS/Linux
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

Create a `.env` file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key_here
```

### 5. Run the app

```bash
streamlit run main.py
```

## 🎯 How It Works

1. **Login** with a unique username to start a session
2. **Select an exercise** from the sidebar (Squats, Push-ups, Biceps Curls, Shoulder Press, Lunges)
3. **Allow webcam access** — the app streams your video and overlays pose landmarks in real time
4. Each detector module calculates relevant joint angles (e.g., knee angle for squats, elbow angle for curls) to:
   - Count reps
   - Detect form issues (e.g., depth, alignment, swing)
5. The **AI Coach** analyzes your form and provides real-time voice feedback via the Groq LLM + TTS pipeline
6. Your session metrics are saved to a local SQLite database for tracking progress over time

## 📋 Requirements

See `requirements.txt`:

```
streamlit==1.54.0
streamlit-webrtc==0.64.5
mediapipe>=0.10.30
opencv-python-headless==4.10.0.84
pandas==2.2.3
groq>=0.12.0
gtts==2.5.3
python-dotenv==1.2.2
```

## 📝 Notes

- A webcam and microphone (for audio playback) are required
- A valid [Groq API key](https://console.groq.com/) is needed for the AI coaching feature
- The app runs best on Python 3.11+ with the latest MediaPipe versions

## 👩‍💻 Author

Built by [Sushma Shukla](https://github.com/Cherry-Syrina)
