---
label: Resume Analyzer AI
icon: briefcase
description: "AI-powered resume/job match tool using LLaMA 3, Groq API, Cloudflare Workers, and React + Vite."
order: 96
tags: [React, Vite, Groq, LLaMA3, Cloudflare-Workers, TypeScript]
---

# Resume Analyzer AI

![](https://img.shields.io/badge/React-18-blue?logo=react)
![](https://img.shields.io/badge/Vite-5.x-blueviolet?logo=vite)
![](https://img.shields.io/badge/TypeScript-5.x-informational?logo=typescript)
![](https://img.shields.io/badge/Groq-LLM-70B-critical?logo=openai)
![](https://img.shields.io/badge/Cloudflare-Workers-orange?logo=cloudflare)

> **Resume Analyzer AI** uses the blazing-fast **LLaMA3-70B model via Groq API** to evaluate how well a resume aligns with a job description — showing strengths, weaknesses, and a smart match score. Serverless and modern, it's built with **Cloudflare Workers** and **React + Vite**.

---

## 🚀 Key Features

| Feature               | Description                                                       |
|-----------------------|-------------------------------------------------------------------|
| 🧠 LLM-Powered         | Uses Groq's LLaMA3-70B for intelligent, JSON-structured analysis |
| 📊 Structured Output   | Returns strengths, weaknesses, score, and recommendations         |
| ⚡ Serverless Infra     | Backend deployed on Cloudflare Workers for ultra-low latency     |
| 🎨 Beautiful Frontend   | UI built with React, Tailwind CSS, and Lucide icons              |
| 🌱 Open Source Ready   | Easily extendable with clear structure and MIT license           |

---

## ⚙️ Architecture Workflow

```mermaid
flowchart LR
    %% Styling
    classDef user fill:#f9f,stroke:#333;
    classDef frontend fill:#6af,stroke:#333;
    classDef backend fill:#f96,stroke:#333;
    classDef api fill:#8f8,stroke:#333;
    classDef data fill:#ff8,stroke:#333;

    %% Nodes
    A[("🗂️ User Uploads<br>Resume & Job Desc")]:::user
    B[["Frontend<br>(React + Vite)"]]:::frontend
    C[["Cloudflare<br>Worker"]]:::backend
    D[["Groq API<br>(LLaMA 3 70B)"]]:::api
    E[["Structured<br>JSON Data"]]:::data
    F[["Analysis<br>Engine"]]:::backend
    G[["Results Dashboard<br>(Score + Feedback)"]]:::frontend

    %% Connections
    A -->|Submit| B
    B -->|API Call| C
    C -->|Query| D
    D -->|JSON Response| E
    E -->|Parse| F
    F -->|Render| G

    %% Optional: Group related nodes
    subgraph User
        A
    end
    subgraph Frontend
        B
        G
    end
    subgraph Backend
        C
        F
    end
    subgraph AI
        D
    end
```

---

## 🗂 Project Structure

```text
resume-analyzer/
├── frontend/
│   ├── src/components/         # UI components like Hero, Inputs, Results
│   ├── src/services/api.ts     # API handler for /analyze call
│   ├── main.tsx, index.css     # App entry and global styles
│   └── .env                    # VITE_API_BASE_URL config
│
├── backend/
│   ├── src/index.ts            # Cloudflare Worker handler
│   ├── wrangler.toml           # Worker configuration
│   └── .dev.vars               # Local dev API key env vars
│
├── LICENSE
├── SECURITY.md
├── CODE_OF_CONDUCT.md
└── README.md
```

---

## 📦 Setup & Run Locally

### ✅ Clone & Navigate

```bash
git clone https://github.com/vxrachit/resume-analyzer.git
cd resume-analyzer
```

### 🎨 Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

Visit: [http://localhost:5173](http://localhost:5173)

### 🟧 Backend (Cloudflare Workers)

```bash
cd ../backend
npx wrangler dev
```

> Make sure `.dev.vars` contains your `GROQ_API_KEY`

---

## 🔐 Add Secrets for Deployment

```bash
npx wrangler secret put GROQ_API_KEY
```

To deploy the worker:

```bash
npx wrangler publish
```

---

## 📡 API Reference

### POST `/analyze`

Send resume and job description as plain text.

#### Request:

```json
{
  "resume_text": "Experienced React developer...",
  "job_description": "Frontend Engineer with React, Vite..."
}
```

#### Response:

```json
{
  "strengths": ["Strong React experience", "Vite familiarity"],
  "weaknesses": ["No backend exposure"],
  "match_score": 78,
  "conclusion": "Strong fit for UI roles, backend knowledge can be improved."
}
```

---

## 🌐 Deployment Recommendations

| Part      | Platform       | Command/Note                      |
|-----------|----------------|----------------------------------|
| Frontend  | Cloudflare / Vercel / Netlify | Deploy via GitHub                |
| Backend   | Cloudflare     | `wrangler publish`                |

---

## 🔐 License

MIT License — free to use, modify, and share.

---

## 🌱 Future Roadmap

- PDF/Docx Resume upload and parsing  
- Admin dashboard for HR teams  
- Multilingual analysis support  
- Gemini Vision resume parser  

---

## 🔗 GitHub

View Source: [https://github.com/vxrachit/resume-analyzer](https://github.com/vxrachit/resume-analyzer)
