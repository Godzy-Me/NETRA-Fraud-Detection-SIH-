# NETRA — AI-Powered MPLADS Fraud & Anomaly Detection

NETRA is a prototype for monitoring MPLADS works and surfacing potentially suspicious projects using risk indicators, anomaly detection, and an interactive dashboard. It combines a React frontend with a FastAPI backend, scored work-level data, MP scorecards, and a trained Isolation Forest model for live proposal evaluation.

> **Note:** NETRA is a decision-support prototype. Risk flags and anomaly scores indicate records that may warrant review; they are not proof of fraud.

## Features

- **Risk dashboard:** summary of total works, anomaly counts, risk distribution, and selected alert indicators.
- **Watchlist:** browse and filter works by risk and other available fields.
- **District risk analysis:** inspect district-level risk information.
- **MP scorecards:** review MP-level summary metrics.
- **Live evaluation:** submit proposal details for model-based anomaly evaluation.
- **Data-driven backend:** loads the scored MPLADS dataset and MP summary from CSV files.

## Tech Stack

- **Frontend:** React, Vite, React Router, Recharts, Tailwind CSS
- **Backend:** Python, FastAPI, Uvicorn, Pandas
- **ML:** scikit-learn, joblib, Isolation Forest
- **Data:** CSV datasets and serialized model/scaler artifacts

## Project Structure

```text
NETRA(SIH)/
├── backend/
│   ├── app/
│   │   ├── data/          # Dataset loading and inspection
│   │   ├── ml/            # Model loading and live evaluation
│   │   ├── schemas/       # Request schemas
│   │   ├── services/      # Data access services
│   │   └── main.py        # FastAPI application and endpoints
│   └── requirements.txt
├── data/                  # Scored works and MP summary CSVs
├── frontend/              # React/Vite dashboard
├── ml/                    # Trained model and scaler files
└── README.md
```

## Prerequisites

Install the following before running the project:

- Python compatible with the installed backend dependencies
- Node.js and npm
- Git (for version control)

## Run the Backend

Open a terminal at the project root and run:

```bash
cd backend
python -m venv .venv
```

Activate the virtual environment:

**Windows PowerShell**

```powershell
.venv\Scripts\Activate.ps1
```

**Windows Command Prompt**

```bat
.venv\Scripts\activate.bat
```

**macOS/Linux**

```bash
source .venv/bin/activate
```

Then install dependencies and start the API:

```bash
pip install -r requirements.txt
uvicorn app.main:app --reload
```

The API should be available at `http://127.0.0.1:8000`. Interactive API documentation is available at `http://127.0.0.1:8000/docs`.

## Run the Frontend

Open a **second terminal** from the project root:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite in the terminal (commonly `http://localhost:5173`). The frontend API client is currently configured to call `http://127.0.0.1:8000`, so start the backend as well.

## API Endpoints

The backend currently exposes these main endpoints:

| Endpoint | Purpose |
|---|---|
| `GET /` | Basic API status message |
| `GET /api/health` | Health check |
| `GET /api/summary` | Dashboard summary and risk indicators |
| `GET /api/watchlist` | Work watchlist with filtering options |
| `GET /api/district_risk` | District-level risk data |
| `GET /api/mp_scorecards` | MP scorecard data |
| `POST /api/evaluate_live` | Evaluate a submitted proposal |

See `/docs` while the backend is running for the exact request parameters and schemas.

## Data and Model Files

The application expects the following files to be present in the repository at their current paths:

- `data/mplads_scored_results.csv`
- `data/mp_summary.csv`
- `ml/mplads_isoforest.joblib`
- `ml/mplads_scaler.joblib`

Do not move these files without updating the corresponding paths in the backend. Model artifacts can be sensitive to library-version differences; use compatible Python and scikit-learn versions if model-loading warnings or errors occur.

## Important Notes

- Keep the backend and frontend running in separate terminals during local development.
- Do not commit passwords, API keys, tokens, or local `.env` files.
- Dataset and model files are included because the current application expects them locally. Check any event, institutional, or dataset-sharing rules before publishing data publicly.
- This repository describes a prototype and does not replace a formal audit or investigation.

## License

No license has been specified yet. Unless a license is added, the default copyright rules apply to reuse of this project.
