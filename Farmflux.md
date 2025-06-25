---
label: FarmFlux
icon: graph
description: "AI-powered crop advisory and farm-management dashboard with Gemini, FastAPI, Supabase, and a React + Vite frontend."
order: 97
tags: [React, Vite, FastAPI, Supabase, Gemini]
---

# FarmFlux

![](https://img.shields.io/badge/React-18-blue?logo=react)
![](https://img.shields.io/badge/Vite-4.0-blueviolet?logo=vite)
![](https://img.shields.io/badge/TypeScript-5.x-informational?logo=typescript)
![](https://img.shields.io/badge/FastAPI-Python-green?logo=fastapi)
![](https://img.shields.io/badge/Supabase-Postgres-orange?logo=supabase)

:icon-mark-github: **GitHub** · [vxrachit/FarmFlux](https://github.com/vxrachit/FarmFlux){target="_blank"}

> **FarmFlux** brings together soil analysis, crop-disease detection, weather insight, and a Gemini-powered chatbot—helping farmers make informed, data-driven decisions.

---

## :icon-rocket: Feature Highlights

| Category | Details |
| --- | --- |
| 🌤️ **Weather Widget** | Real-time 7-day forecast & hourly breakdown |
| 🌱 **Crop Dashboard** | Planting cycles, growth stages, task tracker |
| 🧪 **Disease Detection** | Gemini Vision detects leaf diseases from photos |
| 🧑‍🌾 **Chatbot** | Natural-language Q&A (Gemini Pro) with citations |
| 📊 **Farm Analytics** | Yield estimates & input-cost tracking |
| 🔐 **Supabase Auth** | Email/password & magic-link login |
| 🌍 **Multi-Language** | English, Hindi |

---

## :icon-device-desktop: Screenshots

+++ Dashboard & Chat  
<div style="display:flex;flex-direction:column;align-items:center;gap:24px">
  <img src="/public/farmflux/1.png" alt="Dashboard overview" style="max-width:460px;width:100%" />
  <img src="/public/farmflux/2.png" alt="Chatbot conversation" style="max-width:460px;width:100%" />
  <img src="/public/farmflux/3.png" alt="Weather widget" style="max-width:460px;width:100%" />
</div>  

+++ Diagnose & Reports  
<div style="display:flex;flex-direction:column;align-items:center;gap:24px">
  <img src="/public/farmflux/4.png" alt="Disease upload" style="max-width:460px;width:100%" />
  <img src="/public/farmflux/5.png" alt="Diagnosis result" style="max-width:460px;width:100%" />
  <img src="/public/farmflux/6.png" alt="Analytics panel" style="max-width:460px;width:100%" />
  <img src="/public/farmflux/7.png" alt="Task manager" style="max-width:460px;width:100%" />
</div>  
+++



---

## :icon-stack: Tech Stack

| :icon-browser: **Frontend** | :icon-server: **Backend** | :icon-lock: **Auth / Data** |
| --- | --- | --- |
| React 18 + Vite + TypeScript | FastAPI (Python 3.11) | Supabase Auth |
| Tailwind CSS  | Gemini 2.0 Flash Model | Row-level security |
| React Router v6 | HTTPX| JWT stored by Supabase |

---

## :icon-file-directory: Project Structure

```text
FarmFlux
├── frontend
│   ├── src/components          # UI Components
│   ├── src/context             # Language & Auth Contexts
│   ├── src/services            # API Calls (weather, auth)
│   └── App.tsx                 # Route definitions
│
├── backend
│   ├── app
│       ├── api/                # Route handlers (FastAPI routers)
│       │   ├── chatbot.py
│       │   ├── crop_recommendation.py
│       │   ├── disease_detection.py
│       │   ├── supabase.py    # Login/Signup routes via Supabase
│       │   └── weather.py
│       │
│       ├── core/               # App configuration & startup logic
│       │   └── config.py
│       │
│       ├── models/             # Pydantic models and data schemas
│       │   ├── chatbot.py
│       │   ├── crop_recommendation.py
│       │   ├── disease_detection.py
│       │   ├── supabase.py
│       │   └── weather.py
│       │
│       └── services/           # External service utilities (OpenAI, Weather, etc.)
│       │    ├── gemini_services.py
│       │    ├── supabase_client.py
│       │    └── weather_services.py
│       │
│       └── main.py                 # FastAPI app startup & route includes
│
├── requirements.txt            # Python dependencies
├── .env                        # Environment variables (DO NOT COMMIT)
└── README.md                   # Project documentation
```

---

## :icon-package: Setup & Run Locally

```bash
# 1 clone repo
git clone https://github.com/vxrachit/FarmFlux.git && cd FarmFlux

# 2 backend
cd backend
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000

# 3 frontend
cd ../frontend
npm install
npm run dev
```

Open **http://localhost:5173** and configure your **Gemini** and **Supabase** keys in the respective `.env` files.

---

## :icon-shield-lock: Authentication Flow

```text
React login form ➜ POST /api/login ➜ FastAPI proxy ➜ Supabase Auth ➜ JWT ➜ localStorage ➜ protected routes
```

---

## :icon-milestone: Upcoming

- Batch image upload for multi-leaf diagnosis  
- Offline TensorFlow.js fallback for field use  
- Crop-rotation planner & expense ledger  
- SMS push alerts in rural networks  

---

## :icon-law: License

MIT © {{ year }} **Rachit Verma** — free to fork & adapt.
