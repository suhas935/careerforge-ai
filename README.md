# ⚡ CareerForge AI
### AI-Powered Internship Recommendation & Career Development Platform

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Django](https://img.shields.io/badge/Django-5.2-green)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Railway-blue)
![Groq](https://img.shields.io/badge/Groq-LLaMA%203.1-orange)
![Deploy](https://img.shields.io/badge/Deployed-Railway-purple)
![License](https://img.shields.io/badge/License-MIT-yellow)

> A full-stack AI-powered career platform built for Computer Science students to streamline their placement preparation — from resume analysis to mock interviews, all in one place.

🌐 **Live Demo:** [careerforge-ai-production-d453.up.railway.app](https://careerforge-ai-production-d453.up.railway.app)

---

## 📸 Screenshots

| Dashboard | Resume Analyzer |
|-----------|----------------|
| ![Dashboard](Screenshot%202026-08-17%20160433.png) | ![Resume](Screenshot%202026-08-17%20160459.png) |

| Internship Recommendations | Skill Gap Analysis |
|---------------------------|-------------------|
| ![Internships](Screenshot%202026-08-17%20160534.png) | ![Skills](Screenshot%202026-08-17%20160616.png) |
---

## ✨ Features

| Module | Description |
|--------|-------------|
| 📄 **Resume Analyzer** | Upload PDF resume → AI extracts text → scores 0-100 with strengths, weaknesses & feedback |
| 💼 **Internship Recommendations** | AI matches resume to 5 personalized internship roles with direct apply links (Internshala, Naukri, LinkedIn, Indeed) |
| 🧠 **Skill Gap Analysis** | Compare your skills vs target role → see what you have, what's missing, and free resources to learn |
| 🗺️ **Learning Roadmap** | Week-by-week personalized learning plan with tasks, milestones, and resources |
| 🎯 **Interview Generator** | 10 role-specific questions (Technical, DSA, HR, System Design) with model answers |
| 🤖 **AI Interview Chatbot** | Two modes — Mock Interviewer (asks questions + gives feedback) and Q&A Assistant |
| 📋 **Application Tracker** | Kanban board to track applications (Applied → Shortlisted → Interview → Offer → Rejected) |
| 🏆 **Placement Readiness Score** | Overall 0-100 score based on resume, skills, and activity with action plan |
| 🏠 **Dashboard** | Live stats — placement score, applications count, skill readiness at a glance |
| 🔐 **Authentication** | Register, Login, Logout with Django's built-in auth system |

---

## 🛠️ Tech Stack

### Backend
- **Python 3.10** — Core language
- **Django 5.2** — Web framework (MVT architecture)
- **Django REST Framework** — API support
- **Groq LLaMA 3.1 API** — AI/LLM for all intelligent features
- **PyPDF2** — PDF text extraction

### Database & Storage
- **PostgreSQL** — Production database (Railway)
- **SQLite** — Local development database
- **Cloudinary** — Resume PDF cloud storage

### Frontend
- **Django Templates** — Server-side rendering
- **Tailwind CSS (CDN)** — UI styling
- **Vanilla JavaScript** — Chatbot interactivity

### Deployment
- **Railway** — Backend + PostgreSQL hosting
- **Gunicorn** — WSGI server
- **WhiteNoise** — Static file serving

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- Git
- Groq API Key (free at [console.groq.com](https://console.groq.com))
- Cloudinary account (free at [cloudinary.com](https://cloudinary.com))

### 1. Clone the repository
```bash
git clone https://github.com/suhas935/careerforge-ai.git
cd careerforge-ai
```

### 2. Create virtual environment
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Create `.env` file
```env
SECRET_KEY=your-django-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
GROQ_API_KEY=your-groq-api-key
CLOUDINARY_CLOUD_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-cloudinary-api-key
CLOUDINARY_API_SECRET=your-cloudinary-api-secret
```

### 5. Run migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Start the server
```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000` — register an account and start using CareerForge AI!

---

## 📁 Project Structure

```
careerforge-ai/
│
├── config/                  # Django project settings & URLs
│   ├── settings.py
│   └── urls.py
│
├── accounts/                # Auth — Register, Login, Dashboard
├── resume/                  # Resume Upload & AI Analyzer
├── internships/             # Internship Recommendations
├── skills/                  # Skill Gap Analysis
├── roadmap/                 # Learning Roadmap Generator
├── interview/               # Interview Questions + AI Chatbot
├── tracker/                 # Application Tracker (Kanban)
├── score/                   # Placement Readiness Score
│
├── services/
│   └── claude_service.py    # Central Groq API service
│
├── templates/               # All HTML templates
│   ├── base.html
│   ├── base_auth.html
│   ├── dashboard/
│   ├── resume/
│   ├── internships/
│   ├── skills/
│   ├── roadmap/
│   ├── interview/
│   ├── tracker/
│   └── score/
│
├── static/                  # CSS & JS files
├── requirements.txt
├── Procfile                 # Railway deployment
├── railway.json
└── .env                     # Environment variables (not in git)
```

---

## 🔑 Environment Variables

| Variable | Description |
|----------|-------------|
| `SECRET_KEY` | Django secret key |
| `DEBUG` | True for local, False for production |
| `ALLOWED_HOSTS` | Comma-separated allowed hosts |
| `GROQ_API_KEY` | Groq API key for LLaMA 3.1 |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret |
| `DATABASE_URL` | PostgreSQL URL (auto-set by Railway) |
| `RAILWAY_ENVIRONMENT` | Set to `production` on Railway |

---

## 🌐 Deployment on Railway

1. Push code to GitHub
2. Create new project on [Railway](https://railway.app)
3. Deploy from GitHub repo
4. Add PostgreSQL service
5. Link `DATABASE_URL` to your service
6. Add all environment variables
7. Generate domain under Settings → Networking

---

## 🤖 How the AI Works

All AI features go through a single service function:

```python
# services/claude_service.py
def ask_claude(prompt: str, system: str = "", max_tokens: int = 1500) -> str:
    client = Groq(api_key=os.getenv('GROQ_API_KEY'))
    response = client.chat.completions.create(
        model="llama-3.1-8b-instant",
        messages=[...],
        max_tokens=max_tokens,
    )
    return response.choices[0].message.content
```

Each module sends a structured prompt asking for JSON output, which is then parsed and stored in PostgreSQL.

---

## 📊 Module Flow

```
User registers/logs in
        ↓
Uploads Resume PDF
        ↓
PyPDF2 extracts text → Groq LLaMA analyzes → Score + Feedback stored
        ↓
Internship Recommendations → AI matches resume to roles → Apply links
        ↓
Skill Gap Analysis → AI compares skills vs target role → Learning resources
        ↓
Learning Roadmap → Week-by-week plan generated
        ↓
Interview Prep → 10 questions + AI chatbot for practice
        ↓
Application Tracker → Track applications in Kanban board
        ↓
Placement Score → Overall readiness 0-100 + Action plan
```

---

## 👨‍💻 Author

**Suhas G**
- 📧 suhasg0903@gmail.com
- 🔗 [linkedin.com/in/suhasg0305](https://linkedin.com/in/suhasg0305)
- 🐙 [github.com/suhas935](https://github.com/suhas935)

---

## 📄 License

This project is licensed under the MIT License.

---

## ⭐ Show your support

If you found this project helpful, please give it a ⭐ on GitHub!

---

> Built with ❤️ by Suhas G — SJB Institute of Technology, Bengaluru
