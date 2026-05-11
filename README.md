<div align="center">

# 🌿 Aarogyan
### AI-Powered Personal Health Companion

*A full-stack mobile health application unifying your complete medical history, an intelligent AI doctor, emotional wellness companion, and consultation tracker — all in one place.*

![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.135-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-llama--3.3--70b-F55036?style=for-the-badge&logo=groq&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-1A6B5A?style=for-the-badge)

**[Live API](https://shreyashd111-may-aarogyan.hf.space/api/v1)** · **[API Docs](https://shreyashd111-may-aarogyan.hf.space/docs)**

</div>

---

## 📑 Table of Contents

- [✨ Features](#-features)
- [🛠 Tech Stack](#-tech-stack)
- [🏗 Architecture](#-architecture)
- [📁 Project Structure](#-project-structure)
- [📡 API Reference](#-api-reference)
- [🗄 Database Schema](#-database-schema)
- [🚀 Getting Started](#-getting-started)
- [🔐 Environment Variables](#-environment-variables)
- [☁️ Deployment](#️-deployment)
- [🎨 Design System](#-design-system)
- [📱 App Showcase](#-app-showcase)

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🩺 Health Profile
Maintain a comprehensive medical profile across **9 structured sections**:
- Personal info (DOB, sex, height, weight, blood group, city)
- Existing conditions with severity and diagnosis year
- Allergies (type, reaction, severity)
- Current medications and supplements
- Past medical and surgical history
- Family medical history
- Lifestyle data (activity, diet, sleep, smoking/alcohol)
- Mental health information
- Emergency contact details

</td>
<td width="50%">

### 📋 Consultation Tracker
Organise all your doctor interactions:
- Group visits under named consultations (e.g. *"Diabetes Management 2025"*)
- Log sessions with visit date, symptoms, diagnosis, medications, and notes
- Attach prescription images or lab report PDFs — text auto-extracted via OCR
- Download a fully formatted **PDF report** of any consultation

</td>
</tr>
<tr>
<td width="50%">

### 🤖 AI Medical Assistant
A personalised LLM-powered health chatbot:
- Chat history preserved across sessions in named conversations
- Uses your **full health profile** as context in every response
- **RAG pipeline** queries Qdrant vector DB for evidence-grounded answers
- LLM router distinguishes general vs. detailed queries
- Supports **English, Hindi, and Marathi**
- Powered by Groq `llama-3.3-70b-versatile`

</td>
<td width="50%">

### 📄 Document Summariser
Instantly understand any medical document:
- Upload PDF, JPG, or PNG prescriptions or lab reports
- **EasyOCR + PyMuPDF** extracts raw text (including handwritten prescriptions)
- AI returns structured summary with: `document_type`, `explanation`, `key_findings`, `action_items`, `disclaimer`

</td>
</tr>
<tr>
<td width="50%">

### 🎙️ Emotional Buddy — Orbz
A voice-first emotional wellness companion:
- Hold a **voice conversation** — Whisper transcribes your audio, Orbz responds with synthesised speech via OpenAI TTS
- Select from **12 voice personas** (6 female, 6 male) with preview samples
- Supports text conversation as well as voice
- **Dual emotion detection**: ML text model + Wav2Vec2 audio model fused together
- Mood score (1–10) logged for every interaction

</td>
<td width="50%">

### 📊 Mental Health Dashboard
Visualise emotional wellness over time:
- Daily, weekly, and monthly average mood score charts
- Emotion distribution breakdown (happy / sad / angry / neutral)
- Session history with conversation previews
- Configurable time window: **7 / 30 / 90 days / all time**

</td>
</tr>
</table>

---

## 🛠 Tech Stack

### Backend · Python 3.13

| Category | Technology | Purpose |
|---|---|---|
| **Framework** | FastAPI 0.135 | REST API, async handling, auto OpenAPI docs |
| **Server** | Uvicorn + uvloop | High-performance ASGI server |
| **Database** | Supabase (PostgreSQL) | All structured data storage |
| **File Storage** | Supabase Storage | Uploaded PDFs and images |
| **Auth** | JWT (python-jose) + bcrypt | Stateless token auth, secure password hashing |
| **LLM Inference** | Groq API | `llama-3.3-70b-versatile` for chat, summarisation, routing |
| **Vector DB** | Qdrant Cloud | Semantic search over medical knowledge base |
| **Embeddings** | `BAAI/bge-small-en-v1.5` | Query embeddings for RAG pipeline |
| **Reranker** | `cross-encoder/ms-marco-MiniLM-L-6-v2` | Precision reranking of Qdrant results |
| **OCR** | EasyOCR + PyMuPDF | Text extraction from docs and handwritten prescriptions |
| **Speech-to-Text** | OpenAI Whisper API | Transcribes voice audio to text |
| **Text-to-Speech** | OpenAI TTS API | Synthesises Orbz's voice responses |
| **Emotion Detection** | HuggingFace Transformers + Wav2Vec2 | Text and audio emotion classification |
| **PDF Generation** | fpdf2 | Formatted consultation PDF reports |
| **Config** | pydantic-settings | Typed env-var loading from `.env` |

### Frontend · Dart / Flutter 3.x

| Category | Technology | Purpose |
|---|---|---|
| **State Management** | Riverpod 2 (code-gen) | App-wide reactive state with `riverpod_generator` |
| **HTTP Client** | Dio 5 | API requests with automatic JWT auth interceptor |
| **Routing** | GoRouter 14 | Declarative navigation with auth-guard redirects |
| **Secure Storage** | flutter_secure_storage | JWT token and user_id encrypted on device |
| **Local Prefs** | shared_preferences | Light/dark theme persistence |
| **Fonts** | Google Fonts (DM Sans) | App-wide typography |
| **Charts** | fl_chart | Mood trend and emotion distribution charts |
| **Audio** | record + just_audio + audioplayers | Voice capture and playback for Orbz |
| **Voice Activity** | vad | Voice activity detection |
| **PDF / Printing** | pdf + printing | PDF export and share |
| **Animations** | lottie + flutter_animate | UI motion and loading states |
| **File Handling** | file_picker + image_picker | Document upload flows |
| **Code Generation** | build_runner, freezed, json_serializable, retrofit_generator | Boilerplate generation |

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────┐
│                 Flutter App                     │
│   Riverpod state → Dio (JWT interceptor)        │
│   GoRouter → auth-guarded screens               │
└──────────────────┬──────────────────────────────┘
                   │  HTTPS  /api/v1
┌──────────────────▼──────────────────────────────┐
│              FastAPI Backend                    │
│   9 Routers  →  Services layer                  │
│  ┌──────────┐  ┌──────────┐  ┌───────────────┐ │
│  │ JWT Auth │  │   Groq   │  │   EasyOCR     │ │
│  └────┬─────┘  └────┬─────┘  └───────┬───────┘ │
│       │             │                │          │
│  ┌────▼─────────────▼────────────────▼────────┐ │
│  │           Supabase (PostgreSQL)            │ │
│  │  users · profiles · consultations          │ │
│  │  sessions · conversations · messages       │ │
│  │  emotional_sessions · session_documents    │ │
│  └────────────────────────────────────────────┘ │
│  ┌───────────────┐  ┌────────────────────────┐  │
│  │  Qdrant Cloud │  │  Supabase Storage      │  │
│  │  (RAG vectors)│  │  (PDFs / images)       │  │
│  └───────────────┘  └────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

### AI Chat Request Flow

| Step | Action |
|------|--------|
| **1** | Flutter sends user message with JWT token |
| **2** | FastAPI extracts `user_id` from JWT → loads full health profile from Supabase |
| **3** | LLM router classifies query as **General** or **Detailed** |
| **4** | For Detailed: embeds query → searches Qdrant → reranks hits → builds RAG context |
| **5** | Groq LLM generates response using profile + RAG context + conversation history |
| **6** | Response + message persisted to `messages` and `conversations` tables |
| **7** | Response returned to Flutter for display |

---

## 📁 Project Structure

### Backend · `Backend/`

```
Backend/
├── main.py                         ← App entry, router registration, CORS, RAG warm-up
├── requirements.txt                ← All Python dependencies (pinned versions)
├── Dockerfile                      ← Container build for deployment
├── supabase_schema.sql             ← Full PostgreSQL schema
└── app/
    ├── config.py                   ← pydantic-settings: loads all env vars
    ├── database.py                 ← Supabase client singleton (service-role key)
    ├── auth.py                     ← bcrypt hashing, JWT create/decode, FastAPI Depends
    ├── routers/
    │   ├── auth.py                 ← POST /auth/signup, /auth/login
    │   ├── profile.py              ← GET/PUT /profile/me
    │   ├── consultations.py        ← CRUD /consultations
    │   ├── sessions.py             ← CRUD sessions + document upload/delete
    │   ├── assistant.py            ← Conversation management + /assistant/chat
    │   ├── documents.py            ← POST /documents/summarise
    │   ├── buddy.py                ← Voice + text emotional companion (Orbz)
    │   ├── mental_health.py        ← GET /mental-health/dashboard
    │   └── export.py               ← GET /export/consultation/{id}/pdf
    └── services/
        ├── ai.py                   ← All Groq LLM calls: chat, summarise, buddy, router
        ├── rag_pipeline.py         ← RAG: embed → Qdrant search → rerank → context
        ├── ocr.py                  ← EasyOCR + PyMuPDF text extraction
        ├── stt.py                  ← OpenAI Whisper STT
        ├── tts.py                  ← OpenAI TTS (Sarvam fallback)
        ├── emotion_detection.py    ← Text + audio emotion ML models
        ├── fusion_engine.py        ← Fuses text and audio emotion probabilities
        ├── voice_features.py       ← Extracts acoustic voice features for context
        ├── pdf_export.py           ← fpdf2 formatted consultation PDF
        ├── consultation_pdf_service.py  ← Background PDF rebuild trigger
        ├── profile_context.py      ← Serialises user profile to plain-text for LLM
        └── session_analytics.py    ← Per-session mood/emotion aggregation
```

### Frontend · `lib/`

```
lib/
├── main.dart                       ← App entry: ProviderScope, MaterialApp, theme
└── src/
    ├── core/
    │   ├── network/
    │   │   ├── dio_client.dart     ← Dio instance, JWT interceptor, base URL
    │   │   └── token_storage.dart  ← flutter_secure_storage wrapper
    │   ├── router/
    │   │   └── app_router.dart     ← GoRouter routes + auth-redirect guard
    │   └── theme/
    │       ├── app_theme.dart      ← Material 3 light/dark theme, DM Sans, teal palette
    │       └── theme_provider.dart ← Riverpod notifier, persists theme choice
    ├── features/
    │   ├── auth/                   ← Login, signup, splash
    │   ├── home/                   ← Bottom-nav shell + dashboard
    │   ├── profile/                ← Multi-step profile setup + view/edit
    │   ├── consultation/           ← Consultation list, detail, session detail
    │   ├── assistant/              ← Conversation list + AI chat screen
    │   ├── document/               ← Document upload + summary display
    │   ├── buddy/                  ← Orbz voice companion UI
    │   └── mental_health/          ← Mood charts + session history
    └── shared/
        └── widgets/
            ├── app_button.dart     ← Reusable styled button
            ├── app_text_field.dart ← Reusable styled text input
            └── section_header.dart ← Reusable section title widget
```

---

## 📡 API Reference

All endpoints are prefixed with `/api/v1`. Protected endpoints require:

```
Authorization: Bearer <JWT_TOKEN>
```

### 🔑 Authentication · `/api/v1/auth`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `POST` | `/auth/signup` | Public | Register a new account. Body: `{email, password, full_name}`. Returns `{token, user_id}` |
| `POST` | `/auth/login` | Public | Login with credentials. Body: `{email, password}`. Returns `{token, user_id}` |

### 👤 Profile · `/api/v1/profile`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `GET` | `/profile/me` | Required | Fetch the full health profile for the logged-in user |
| `PUT` | `/profile/me` | Required | Create or update (upsert) any profile fields. All fields optional |

### 📋 Consultations · `/api/v1/consultations`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `GET` | `/consultations/` | Required | List all consultations for the user |
| `POST` | `/consultations/` | Required | Create a consultation. Body: `{name, start_date?, notes?}` |
| `GET` | `/consultations/{id}` | Required | Get a single consultation with all sessions |
| `PATCH` | `/consultations/{id}` | Required | Update consultation fields |
| `DELETE` | `/consultations/{id}` | Required | Delete a consultation and all its sessions |

### 🗓 Sessions · `/api/v1/consultations/{consultation_id}/sessions`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `GET` | `/sessions/` | Required | List all sessions with attached documents |
| `POST` | `/sessions/` | Required | Create a session with visit date, symptoms, diagnosis, and notes |
| `GET` | `/sessions/{id}` | Required | Get a single session with all documents |
| `PATCH` | `/sessions/{id}` | Required | Update session fields |
| `DELETE` | `/sessions/{id}` | Required | Delete session and its documents |
| `POST` | `/sessions/{id}/documents` | Required | Upload PDF/JPG/PNG — OCR extracted automatically |
| `DELETE` | `/sessions/{id}/documents/{doc_id}` | Required | Delete document from DB and Storage |

### 🤖 Medical Assistant · `/api/v1/assistant`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `GET` | `/assistant/conversations` | Required | List all named conversations |
| `POST` | `/assistant/conversations` | Required | Create a new conversation thread |
| `GET` | `/assistant/conversations/{id}` | Required | Get conversation with full message history |
| `DELETE` | `/assistant/conversations/{id}` | Required | Delete a conversation |
| `POST` | `/assistant/chat` | Required | Send message. Body: `{message, conversation_id?, preferred_language?}`. Returns AI response |

> **Chat flow:** Loads health profile → classifies query (general/detailed) → for detailed: embeds + Qdrant search + rerank → Groq generates response → persists to DB → returns to Flutter.

### 📄 Document Summarisation · `/api/v1/documents`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `POST` | `/documents/summarise` | Required | Upload PDF/JPG/PNG (max 1.5 MB). Returns `{ocr_text, summary}` with `document_type`, `explanation`, `key_findings`, `action_items`, `disclaimer` |

### 🎙️ Emotional Buddy (Orbz) · `/api/v1/buddy`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `POST` | `/buddy/voice` | Required | Upload audio → STT → AI response → TTS. Returns `{transcript, buddy_text, mood_score, audio_base64}` |
| `POST` | `/buddy/text` | Required | Text message → empathetic AI response. Body: `{text, history?, preferred_language?, session_group_id?}` |
| `GET` | `/buddy/sessions` | Required | List all buddy sessions |
| `GET` | `/buddy/sessions/{id}` | Required | Get single buddy session |
| `GET` | `/buddy/voices` | Required | List available TTS voice catalogue |
| `GET` | `/buddy/voices/{voice_id}/sample` | Required | Get audio preview of a voice persona |

### 📊 Mental Health Dashboard · `/api/v1/mental-health`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `GET` | `/mental-health/dashboard?days=30` | Required | Returns aggregated mood data: daily scores, weekly/monthly averages, emotion distribution, recent sessions. `days=0` = all-time |

### 📥 Export · `/api/v1/export`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `GET` | `/export/consultation/{id}/pdf` | Required | Download complete consultation report as formatted PDF. Serves cached PDF from Supabase Storage or generates on-demand |

---

## 🗄 Database Schema

The full schema is in [`Backend/supabase_schema.sql`](Backend/supabase_schema.sql). Run it in the Supabase SQL editor to provision all tables, indexes, and policies.

| Table | Description |
|-------|-------------|
| `users` | Core user accounts — email, password hash, full name |
| `profiles` | Comprehensive health profile: personal info + 8 JSONB sections |
| `consultations` | Named consultation groups per user |
| `sessions` | Individual doctor visit records inside a consultation |
| `session_documents` | Uploaded files with OCR text and Supabase Storage path |
| `conversations` | AI chat threads, named and timestamped per user |
| `messages` | Individual messages within a conversation (user + assistant roles) |
| `emotional_sessions` | Buddy interactions with mood score, emotion probabilities, audio metadata |

---

## 🚀 Getting Started

### Prerequisites

- **Flutter SDK** ≥ 3.5
- **Python** 3.11+
- A [Supabase](https://supabase.com) project *(free tier works)*
- A [Groq](https://console.groq.com) API key *(free tier available)*
- A [Qdrant Cloud](https://cloud.qdrant.io) cluster *(free tier available)*
- An [OpenAI](https://platform.openai.com) API key *(for Whisper STT + TTS)*

---

### Step 1 — Supabase Setup

1. Create a new Supabase project.
2. Open the **SQL Editor** and run the full contents of [`Backend/supabase_schema.sql`](Backend/supabase_schema.sql).
3. Create two **private** storage buckets:
   - `documents` — for session document uploads
   - `pdfs` — for exported consultation PDFs
4. Note your **Project URL**, **Service Role Key**, and **Anon Key** from *Project Settings → API*.

---

### Step 2 — Backend Setup

```bash
cd Backend

# Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env
# Edit .env with your credentials (see Environment Variables section)

# Start the development server
uvicorn main:app --reload --port 8000
```

API available at `http://localhost:8000`  
Interactive docs at `http://localhost:8000/docs` *(development mode only)*

---

### Step 3 — Flutter Setup

```bash
# From the project root
flutter pub get

# Generate code (Riverpod, Freezed, Retrofit, JSON serializers)
dart run build_runner build --delete-conflicting-outputs

# Run the app
flutter run
```

> **Android Emulator:** The Dio client is pre-configured to use `http://10.0.2.2:8000/api/v1` which maps to your localhost from within the emulator.
>
> **Physical device:** Update `baseUrl` in `lib/src/core/network/dio_client.dart` to your machine's local IP (e.g. `http://192.168.x.x:8000/api/v1`).

---

## 🔐 Environment Variables

Copy `Backend/.env.example` to `Backend/.env` and fill in all values.

> ⚠️ **Never commit `.env`** — it is already listed in `.gitignore`.

```env
# ── Supabase ────────────────────────────────────────────────────
SUPABASE_URL=https://your-project-ref.supabase.co
SUPABASE_SERVICE_ROLE_KEY=eyJ...          # Project Settings → API
SUPABASE_ANON_KEY=eyJ...

# ── Groq (LLM) ─────────────────────────────────────────────────
GROQ_API_KEY=gsk_...
GROQ_MODEL=llama-3.3-70b-versatile

# ── Qdrant (Vector DB for RAG) ─────────────────────────────────
QDRANT_URL=https://your-cluster.qdrant.io
QDRANT_API_KEY=...
QDRANT_COLLECTION=medical_rag

# ── OpenAI (Whisper STT + TTS) ─────────────────────────────────
OPENAI_API_KEY=sk-...

# ── Optional: Sarvam (Indian language TTS fallback) ────────────
SARVAM_API_KEY=                           # Leave empty to use OpenAI TTS only

# ── JWT Auth ────────────────────────────────────────────────────
JWT_SECRET_KEY=<generate: openssl rand -hex 32>
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=10080         # 7 days

# ── App ─────────────────────────────────────────────────────────
APP_ENV=development                       # Set to "production" to hide /docs
CORS_ORIGINS=http://localhost,http://localhost:3000,http://10.0.2.2
```

---

## ☁️ Deployment

The backend is live on **HuggingFace Spaces**:

- **Space:** https://huggingface.co/spaces/shreyashd111/may_Aarogyan
- **API Base URL:** `https://shreyashd111-may-aarogyan.hf.space/api/v1`

### Deploy to HuggingFace Spaces

1. Create a new Space with **Docker SDK**.
2. Push the `Backend/` folder contents to the Space repository.
3. Add all environment variables as **Space Secrets**.
4. HuggingFace builds from the `Dockerfile` and starts automatically.

### Deploy to Railway

1. Push the repo to GitHub.
2. Create a new Railway project linked to your GitHub repo.
3. Set all environment variables in the Railway dashboard.
4. Railway builds using the `Dockerfile` and starts the server.

---

## 🎨 Design System

The Flutter app uses a custom **Material 3** theme defined in `lib/src/core/theme/app_theme.dart`. Light and dark themes are both supported, with the user's preference persisted via `shared_preferences`.

| Token | Value | Description |
|-------|-------|-------------|
| **Primary** | `#1A6B5A` | Teal green |
| **Secondary** | `#E8F5F0` | Light teal |
| **Accent** | `#F4845F` | Warm orange |
| **Surface** | `#FFFFFF` | White |
| **Background** | `#F7FAF9` | Off-white |
| **Error** | `#D94F4F` | Red |
| **Text Primary** | `#1A1A2E` | Near black |
| **Text Secondary** | `#6B7280` | Gray |
| **Font** | DM Sans (Google Fonts) | App-wide typography |
| **Border Radius** | 16 – 24 px | Rounded corners |
| **Min Tap Target** | 48 px | Accessibility |

---

📱 App Showcase
<table> <tr> <td width="50%">

Authentication

<img src="assets/Aarogyan_Screenshots/User%20Login%20screen.jpeg" alt="Login Screen" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Registration

<img src="assets/Aarogyan_Screenshots/User%20registration%20Screen.jpeg" alt="Registration Screen" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Home Dashboard

<img src="assets/Aarogyan_Screenshots/Home%20dashboard%20displaying%20quick%20action%20cards%20and%20feature%20navigation%20tiles.jpeg" alt="Home Dashboard" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Health Profile

<img src="assets/Aarogyan_Screenshots/User%20profile%20Dashboard%201.jpeg" alt="Health Profile" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Profile Management

<img src="assets/Aarogyan_Screenshots/User%20profile%20Dashboard%202.jpeg" alt="Profile Dashboard 2" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Profile Overview

<img src="assets/Aarogyan_Screenshots/User%20profile%20Dashboard%203.jpeg" alt="Profile Dashboard 3" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Medical Assistant

<img src="assets/Aarogyan_Screenshots/Medical%20Assistant%20conversation%20list.jpeg" alt="Medical Assistant" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

AI Chat Conversation

<img src="assets/Aarogyan_Screenshots/Multi-turn%20conversation%20with%20medical%20assistant.jpeg" alt="AI Chat" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Consultations

<img src="assets/Aarogyan_Screenshots/Consultations%20Screen.jpeg" alt="Consultations" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Create Consultation

<img src="assets/Aarogyan_Screenshots/Creating%20Consultation.jpeg" alt="Create Consultation" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Session Timeline

<img src="assets/Aarogyan_Screenshots/Session%20Timeline%20Screen.jpeg" alt="Session Timeline" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Create Session

<img src="assets/Aarogyan_Screenshots/Creating%20Session.jpeg" alt="Create Session" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Document Upload

<img src="assets/Aarogyan_Screenshots/Document%20upload%20screen.jpeg" alt="Document Upload" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

AI Document Summary

<img src="assets/Aarogyan_Screenshots/AI-generated%20summary.jpeg" alt="AI Summary" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Key Findings

<img src="assets/Aarogyan_Screenshots/Key%20Findings%20and%20confidence%20score.jpeg" alt="Key Findings" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Emotional Buddy - Idle

<img src="assets/Aarogyan_Screenshots/Emotional%20Buddy%20idle%20screen.jpeg" alt="Emotional Buddy" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Voice Personas

<img src="assets/Aarogyan_Screenshots/Voice%20persona%20selection%20interface%20showing%20multiple%20speakers.jpeg" alt="Voice Personas" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Orbz Thinking

<img src="assets/Aarogyan_Screenshots/Orbz%20in%20active%20thinking%20state.jpeg" alt="Orbz Thinking" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Mental Health Analytics

<img src="assets/Aarogyan_Screenshots/Mental%20Health%20Dashboard%201.jpeg" alt="Mental Health Dashboard 1" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Mood Trends

<img src="assets/Aarogyan_Screenshots/Mental%20Health%20Dashboard%202.jpeg" alt="Mental Health Dashboard 2" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> <tr> <td width="50%">

Emotion Insights

<img src="assets/Aarogyan_Screenshots/Mental%20Health%20Dashboard%203.jpeg" alt="Mental Health Dashboard 3" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> <td width="50%">

Terms & Conditions

<img src="assets/Aarogyan_Screenshots/Terms%20And%20Conditions%20Screen.jpeg" alt="Terms & Conditions" style="max-width:280px; width:100%; border-radius:12px; display:block; margin:auto;"> </td> </tr> </table>

---

## �📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

Built with ❤️ using **Flutter · FastAPI · Supabase · Groq · Qdrant**

</div>
