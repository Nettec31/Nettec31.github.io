# 🚀 Success Lobby
### *Connecting Students. Building Success.*

**Success Lobby** is an AI-powered study partner matching platform built exclusively for CPCC students. It uses smart matching and Google Gemini AI to connect students based on their courses, availability, campus, and study style.

---

## 📋 Project Overview

Many students struggle to find compatible study partners within their specific courses. **Success Lobby** bridges this gap by providing a centralized hub where students can:

- **Get Matched:** Find peers in the same course ranked by compatibility score.
- **Connect Intelligently:** AI reads your study bio and finds students with complementary learning styles.
- **Build Study Groups:** Send and accept connect requests to reveal contact info and start collaborating.

---

## 👥 The Team (Code-Avengers)

| Name | Role |
|---|---|
| **Lynnette Ray** | Project Lead & Lead Product Architect |
| **Juanita Cobos** | Lead UI/UX Developer |
| **Daksh Singh** | Technical Contributor |
| **Urangoo "Uka" Dashdavaa** | System Architect & Backend Developer |

---

*Developed for the CPCC Innovation Challenge.*

---

## 🏗️ Technical Architecture

The **Code-Avengers** collaborated to design a full-stack system that connects student data with the user interface through a secure, AI-powered matching engine.

### The Stack

| Layer | Technology |
|---|---|
| **Backend** | Python + Flask |
| **Database** | SQLite via Flask-SQLAlchemy |
| **Course Data** | JSON file for static course lookups |
| **Frontend** | HTML · CSS · JavaScript |
| **AI Layer** | Google Gemini API |
| **Security** | bcrypt password hashing · CPCC email validation |

### Logic Flow

1. **Authentication:** CPCC email-only registration. Passwords hashed with bcrypt and stored in SQLite — never plain text.
2. **Profile Setup:** Students fill in major, availability, campus preference, and a study bio used for AI matching.
3. **Course Enrollment:** Students type a course code — the name auto-fills from `courses.json` — saved to the `StudentCourse` table.
4. **Lobby:** Students see their enrolled courses and how many peers are active in each course room.
5. **Smart Matching:** Two-layer engine runs when a student enters a course room:
   - Rule-based: same major (+20), same availability (+20), same campus (+20)
   - AI-based: Google Gemini reads both study bios and returns a compatibility reason (+40)
   - Students sorted by highest match percentage first
6. **Connection System:** Students send connect requests saved as `pending` in the database. The partner accepts or declines from their profile page. Email is revealed upon acceptance.

### Database Schema

```
User
├── id, name, email, password (bcrypt)
├── major, availability, campus
└── bio (used for AI matching)

StudentCourse
├── id, email
├── course_code, course_name
└── (linked to User via email)

Connection
├── id, from_email, to_email
├── course_code
└── status (pending / accepted / declined)
```

---

## 🚀 How to Run

1. Make sure **Python 3** is installed.
2. Install dependencies:
   ```bash
   pip install flask flask-sqlalchemy flask-cors bcrypt google-genai
   ```
3. Run the server:
   ```bash
   python app.py
   ```
4. Open `http://127.0.0.1:5000/` to enter the **Success Lobby**.

---

## 📁 Project Structure

```
Success-Lobby/
├── app.py              ← Flask backend — all API routes
├── models.py           ← SQLite database tables
├── courses.json        ← CPCC course code lookup
├── templates/
│   ├── cpcc_login.html ← Register / Sign in
│   ├── profile.html    ← Profile setup + course enrollment
│   ├── lobby.html      ← Active course lobbies
│   ├── room.html       ← Study partner matching
│   └── quiz.html       ← Onboarding quiz
└── instance/
    └── successlobby.db ← SQLite database (auto-created)
```
