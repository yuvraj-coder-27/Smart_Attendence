# 📸 SnapClass - Smart AI Attendance System

> **Making Attendance Faster, Smarter, and Seamless using AI & Biometrics**

SnapClass is an intelligent multi-modal attendance management platform built with **Streamlit**, **Supabase**, **dlib**, **Scikit-Learn**, **Resemblyzer**, and **Librosa**. It eliminates tedious manual roll calls by automating attendance tracking using **Face Recognition** from classroom group photos and **Voice Identification** from speech recordings.

---

## 🚀 Key Features

### 👨‍🏫 Teacher Portal
- **Dashboard & Subject Management**: Create, view, and organize subjects and sections with real-time class metrics.
- **Biometric Face Attendance**: Upload a single classroom photo to automatically detect, recognize, and mark attendance for multiple students simultaneously using an SVM classifier trained on 128-D facial embeddings.
- **Voice Attendance Pipeline**: Upload classroom audio files or individual voice recordings. Audio is split into speech segments using `librosa`, processed into voice embeddings using `Resemblyzer`, and matched against enrolled student voice profiles using cosine similarity.
- **QR Code & Link Enrollment**: Generate subject-specific QR codes (powered by `segno`) and shareable links (`?join-code=...`) for instant student enrollment.
- **Attendance Analytics & Export**: View logs and export detailed attendance data to CSV for record-keeping.

### 👨‍🎓 Student Portal
- **Biometric Enrollment**: Register student profiles with facial images and voice audio clips to generate reference biometric embeddings.
- **Instant Subject Joining**: Join classes seamlessly by scanning QR codes or clicking shared subject invitation links.
- **Personal Attendance Tracking**: Monitor enrolled subjects, attendance rates, and class history.

---

## 🧠 AI & Machine Learning Pipelines

### 1. 👤 Face Recognition Engine (`dlib` + `scikit-learn`)
- **Detector**: `dlib` HOG-based frontal face detector.
- **Landmarks & Feature Extractor**: 68-point shape predictor + 128-dimensional deep face descriptor model.
- **Classifier**: Support Vector Machine (`SVC` with linear kernel & probability outputs) trained dynamically on enrolled student face vectors.
- **Thresholding**: Euclidean distance resemblance thresholding to ensure high accuracy and reduce false positives.

### 2. 🎙️ Voice Identification Engine (`Resemblyzer` + `Librosa`)
- **Audio Preprocessing & Segmentation**: Non-silent audio chunks extracted using `librosa.effects.split` (top_db thresholding).
- **Encoder**: Deep learning speaker encoder (`VoiceEncoder`) from `Resemblyzer` producing d-vector voice embeddings.
- **Matching Algorithm**: Cosine similarity comparison with configurable similarity thresholds ($\ge 0.65$).

---

## 🛠️ Tech Stack

| Category | Technology |
| :--- | :--- |
| **Frontend & App Framework** | [Streamlit](https://streamlit.io/) |
| **Database & Auth** | [Supabase](https://supabase.com/) (PostgreSQL) & `bcrypt` |
| **Face Recognition** | `dlib`, `face_recognition_models`, `scikit-learn` |
| **Voice Recognition** | `resemblyzer`, `librosa` |
| **QR Code Generation** | `segno` |
| **Data & Image Processing** | `numpy`, `pandas`, `Pillow` |


---

## 📖 Usage Guide

### For Teachers:
1. Navigate to the **Teacher Portal**.
2. Sign up or log in.
3. Create subjects with subject code, name, and section.
4. Click **Share** on a subject card to reveal the QR code or invitation URL for students.
5. Take attendance by uploading a **Classroom Photo** (Face Recognition) or an **Audio File** (Voice Recognition).
6. Review attendance results and export logs to CSV.

### For Students:
1. Navigate to the **Student Portal**.
2. Enroll by entering your name, capturing/uploading a face photo, and providing a voice sample.
3. Scan a subject QR code or open a share URL to auto-enroll.
4. View your subject enrollment list and personal attendance history.

