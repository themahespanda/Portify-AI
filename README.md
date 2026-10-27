# Portify AI — Resume-to-Portfolio Website Generator

Portify AI is a full-stack, AI-powered web application that converts static PDF and DOCX resumes into polished, customizable, and recruiter-ready personal portfolio websites.

![Portify AI Banner](https://images.unsplash.com/photo-1507238691740-187a5b1d37b8?auto=format&fit=crop&w=1200&q=80)

---

## 🚀 Key Features

- **Document Parsing Engine**:
  - Direct extraction of structured data from both **PDF** (via PyMuPDF / `pymupdf`) and **DOCX** (via `python-docx`).
  - Scanned PDF detection with explicit user warnings explaining machine-readable text / OCR requirements.
  - Strict preservation of verified facts: never fabricates work experience, employers, metrics, or credentials.

- **Intelligent Content Synthesis**:
  - Deterministic high-quality **Demo Mode** enabled by default (zero API key dependency).
  - Optional **Google Gemini API** integration (`gemini-2.5-flash` via the official `google-genai` SDK) for tailored creative rephrasing and editorial refinement.
  - Generates punchy headlines, engaging multi-paragraph "About Me" narratives, recruiter-focused project impact summaries, and categorized technical skills.
  - Section-by-section AI polishing with custom guidance and tone selection (*Professional*, *Technical*, *Creative*, *Executive*).

- **4 Fully Implemented Portfolio Themes**:
  1. **Modern Minimal**: Clean whitespace, subtle borders, crisp sans-serif typography, and indigo accents.
  2. **Developer Dark**: GitHub-inspired dark aesthetic, monospace typography, terminal badges, and code tags.
  3. **Creative Gradient**: Vibrant purple-to-cyan gradient titles, backdrop-blur cards, and expressive designer layouts.
  4. **Professional Corporate**: Deep navy tones, structured executive grid, and recruiter-friendly authority.

- **Portfolio Builder & Real-time Live Preview**:
  - Drag-and-drop section visibility toggles and reordering arrows for Hero, About, Skills, Projects, Experience, Education, Certifications, and Contact.
  - Instant live sync: all text edits and theme switches reflect immediately.
  - Responsive viewport switchers (*Desktop*, *Tablet 768px*, *Mobile 375px*).

- **Standalone Export & One-Click Deployment**:
  - Generates a standalone, dependency-free ZIP package containing:
    - `index.html`: Fully semantic, responsive portfolio website.
    - `styles.css`: Pure CSS matching the selected theme.
    - `script.js`: Interactive navigation, smooth scrolling, mobile drawer menu, and clipboard copy.
    - `portfolio-data.json`: Portable JSON backup for easy restoration.
    - `README.md`: Step-by-step instructions for zero-cost hosting on GitHub Pages, Netlify Drop, Vercel, and Cloudflare Pages.
  - Double-click `index.html` to view locally in any browser with no server required.

- **Local Storage Persistence & Appearance**:
  - Automatic draft saving to browser `localStorage` ensures work is never lost on refresh.
  - System-aware Light and Dark mode toggle with persisted preference.

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, TypeScript, Vite, Tailwind CSS, Lucide React, JSZip |
| **Backend** | Python 3.11+, FastAPI, Uvicorn, Pydantic v2 |
| **Document Processing** | PyMuPDF (`pymupdf`), `python-docx` |
| **AI Integration** | Google GenAI SDK (`google-genai`), Configurable Gemini API |
| **Storage & Persistence** | Browser `localStorage` (Client-side draft state) |

---

## 📂 Project Structure

```
portify-ai/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.tsx             # Header navigation, theme toggle, mode status
│   │   │   └── LivePreviewFrame.tsx   # Interactive live responsive viewport preview
│   │   ├── pages/
│   │   │   ├── LandingPage.tsx        # Hero, interactive theme preview, features
│   │   │   ├── UploadPage.tsx         # Drag-and-drop resume upload & file validation
│   │   │   ├── AnalysisPage.tsx       # Editable parsed resume review & field manager
│   │   │   └── BuilderPage.tsx        # Dashboard, section editor, AI studio, themes
│   │   ├── services/
│   │   │   └── api.ts                 # FastAPI client endpoints & fallback logic
│   │   ├── types/
│   │   │   └── index.ts               # Complete TypeScript data models
│   │   ├── App.tsx                    # Root routing, draft persistence, state manager
│   │   ├── index.css                  # Tailwind styles and custom utilities
│   │   └── main.tsx                   # React DOM entry point
│   ├── package.json
│   ├── tsconfig.json
│   └── vite.config.ts
├── backend/
│   ├── app/
│   │   ├── models/
│   │   │   ├── resume.py              # Pydantic schema for Resume data
│   │   │   └── portfolio.py           # Pydantic schema for Portfolio & Themes
│   │   ├── routes/
│   │   │   ├── resume.py              # POST /api/resume/parse, GET samples
│   │   │   └── portfolio.py           # POST generate, refine, export ZIP
│   │   ├── services/
│   │   │   ├── parser.py              # PyMuPDF & python-docx parser heuristics
│   │   │   ├── ai_generator.py        # Gemini API & deterministic demo generator
│   │   │   ├── exporter.py            # Standalone HTML/CSS/JS package generator
│   │   │   └── samples.py             # Pre-configured rich resume test profiles
│   │   └── main.py                    # FastAPI application & health route
│   ├── requirements.txt
│   ├── .env.example
│   └── direct_test.py                 # Automated verification test script
└── README.md
```

---

## ⚙️ Quickstart Guide

### 1. Prerequisites
- **Node.js** v18+ and **npm**
- **Python** v3.10+ (or Python 3.11)

---

### 2. Backend Setup

1. Open a terminal and navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Create a Python virtual environment and activate it:
   ```bash
   # Windows PowerShell
   python -m venv venv
   .\venv\Scripts\Activate.ps1

   # macOS / Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

4. Configure environment variables (optional):
   ```bash
   copy .env.example .env
   ```
   *Note: If `GEMINI_API_KEY` is not provided, Portify AI runs in deterministic **Demo Mode** with full feature availability.*

5. Start the FastAPI backend server:
   ```bash
   uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
   ```
   The backend API will be running at `http://127.0.0.1:8000` (API docs at `http://127.0.0.1:8000/docs`).

---

### 3. Frontend Setup

1. In a new terminal, navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the Vite development server:
   ```bash
   npm run dev
   ```
   Open your browser at `http://localhost:5173`.

---

## 🧪 Verification & Automated Testing

You can run the direct backend route verification script at any time:

```bash
cd backend
.\venv\Scripts\python.exe direct_test.py
```

This verifies:
1. `GET /api/health` — returns backend health and AI configuration status.
2. `GET /api/resume/samples/alex-morgan` — returns verified candidate dataset.
3. `POST /api/portfolio/generate` — generates complete portfolio content and sets default theme.
4. `POST /api/portfolio/refine` — tests section-specific AI polish and custom instruction.
5. `POST /api/portfolio/export` — compiles the in-memory standalone website ZIP archive and validates asset integrity.

---

## 🌐 Deploying Your Exported Portfolio

When you click **Download ZIP Website** in Portify AI, your ZIP archive is immediately ready for publishing.

### Option 1: GitHub Pages (Free)
1. Create a new GitHub repo (e.g. `my-portfolio`).
2. Extract the downloaded ZIP and push `index.html`, `styles.css`, and `script.js` to the root of the repository.
3. In GitHub, navigate to **Settings > Pages**.
4. Choose **Deploy from a branch**, select branch `main` and folder `/ (root)`, and click **Save**.
5. Your website is live within 60 seconds at `https://<your-username>.github.io/my-portfolio`.

### Option 2: Netlify Drop (Instant Drag-and-Drop)
1. Go to [Netlify Drop](https://app.netlify.com/drop).
2. Drag and drop the unzipped portfolio folder.
3. Done! Netlify provisions a live HTTPS URL instantly.

---

## 🔒 Privacy & Safety Notice
Portify AI processes documents in-memory and does not store uploaded resume files or contact information to disk. Generated static website code is sanitized to prevent XSS vulnerabilities, and external links are opened with safe `rel="noreferrer noopener"` attributes.
