📊 GitHub Skill Gap Analyzer

A full-stack application that analyzes public GitHub profiles and identifies skill gaps relative to target software engineering roles.

This tool helps developers understand:
- How job-ready their GitHub portfolio is
- Strengths across repositories
- Missing skills for specific roles (Backend, Frontend, SWE Intern, etc.)
- Concrete improvement recommendations

⸻

🚀 Tech Stack

**Backend**
- FastAPI – REST API framework
- SQLAlchemy – ORM for database modeling
- PostgreSQL – Data persistence
- httpx – GitHub API requests
- Docker – Database containerization

**Frontend**
- Next.js (TypeScript) – React framework
- Tailwind CSS – UI styling

⸻

🏗️ System Architecture

User → Frontend (Next.js)
      → Backend API (FastAPI)
            → GitHub REST API
            → PostgreSQL

**Flow Overview**
1. User enters a GitHub username.
2. Backend fetches public repositories via GitHub API.
3. Repository metadata is analyzed and scored.
4. Data is stored in PostgreSQL.
5. Gap analysis is performed against predefined role templates.
6. Frontend displays:
   - Overall score
   - Repo rankings
   - Skill gaps
   - Improvement plan

⸻

📂 Project Structure

github-skill-gap-analyzer/
│
├── backend/
│   ├── app/
│   │   ├── main.py          # FastAPI entry point
│   │   ├── models.py        # SQLAlchemy models
│   │   ├── database.py      # DB connection setup
│   │   ├── github_client.py # GitHub API logic
│   │   ├── scoring.py       # Repo scoring logic
│   │   └── routes/          # API endpoints
│   │
│   ├── requirements.txt
│   └── .env
│
├── frontend/
│   ├── app/
│   ├── components/
│   └── package.json
│
├── docker-compose.yml
└── README.md


⸻

🧠 How the Scoring System Works

Each repository is evaluated using heuristic quality signals.

**Signals Evaluated**

| Signal            | Description                                        |
|-------------------|----------------------------------------------------|
| README Score      | README exists and has sufficient length            |
| Test Score        | Presence of test directory or known test frameworks|
| CI Score          | GitHub Actions workflow exists                     |
| Activity Score    | Recent commit activity                             |
| Contributor Score | Multiple contributors (bus factor proxy)           |
| Language Diversity| Variety of languages used                          |

⸻

Repo Score Formula (Example)

```python
repo_score = (
  (0.2 * readme_score) +
  (0.2 * test_score) +
  (0.15 * ci_score) +
  (0.2 * activity_score) +
  (0.15 * contributor_score) +
  (0.1 * language_score)
)
```

Final repo score is normalized to 0–100.

⸻

🎯 Role-Based Gap Analysis

Each role template defines:
- Required skills
- Nice-to-have skills
- Infrastructure expectations (CI, tests, documentation)

**Example: Backend Intern Template**

```json
{
  "required_languages": ["Python", "Java", "Go"],
  "required_features": ["tests", "ci", "api_design"],
  "nice_to_have": ["docker", "postgres", "aws"]
}
```

The system compares:
- Detected repo stack
- Feature presence
- Project complexity signals

Then outputs:
- Missing skills
- Skill match percentage
- Suggested next projects

⸻

🔄 API Endpoints

**Health Check**

`GET /health`

Returns:

```json
{ "ok": true }
```

⸻

**Start Scan**

`POST /scan`

Body:

```json
{
  "username": "octocat"
}
```

Returns:

```json
{
  "scan_run_id": "uuid"
}
```

⸻

**Get Profile Results**

`GET /profile/{username}`

Returns:
- Overall score
- Repo list
- Repo rankings

⸻

**Get Role Gap Analysis**

`GET /profile/{username}/role/{role_name}`

Returns:
- Match %
- Missing skills
- Improvement suggestions

⸻

🗄️ Database Design

**profiles**

Stores scanned GitHub users.

**repos**

Stores repository metadata.

**repo_metrics**

Stores computed scores for each repository.

**scan_runs**

Tracks scan status and history.

⸻

⚙️ Local Development Setup

**1. Clone repository**

```bash
git clone https://github.com/YOUR_USERNAME/github-skill-gap-analyzer.git
cd github-skill-gap-analyzer
```

⸻

**2. Start Database**

```bash
docker compose up -d
```

⸻

**3. Backend Setup**

```bash
cd backend
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

⸻

**4. Frontend Setup**

```bash
cd frontend
npm install
npm run dev
```

Frontend runs at: `http://localhost:3000`

⸻

🧩 Future Improvements

- AST-based complexity analysis
- Code quality lint scoring
- Commit message NLP analysis
- Machine learning model for job-role prediction
- OAuth login
- Resume PDF parsing
- CI/CD deployment pipeline

⸻

📈 Resume Bullet Point Example

Built a full-stack GitHub analysis platform using FastAPI, PostgreSQL, and Next.js that evaluates repository quality signals and performs role-based skill gap analysis, generating actionable improvement plans.

⸻

🛡️ Rate Limits

GitHub API rate limits:
- 60 requests/hour (unauthenticated)
- 5,000 requests/hour (authenticated)

Add a personal access token in `.env`:

```bash
GITHUB_TOKEN=your_token_here
```

⸻

🎓 Why This Project Matters

This project demonstrates:
- API integration
- Backend architecture
- Database modeling
- Scoring algorithm design
- Frontend dashboard design
- Real-world product thinking

It goes beyond CRUD and shows applied systems thinking.

⸻

If you want next:
- We can now write the GitHub API ingestion module.
- Or implement the scoring algorithm.
- Or design the first database model properly.

Your repo is already looking strong. 🚀

