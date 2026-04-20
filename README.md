# Kyrgyz Root Calendar

Kyrgyz Root Calendar is a full-stack web app for visualizing a traditional Kyrgyz calendar with astronomy-based events and cultural dates.

The backend (FastAPI) calculates:
- Moon phases (new moon, full moon)
- Togool (Moon and Pleiades conjunction-style events)
- Nooruz timing logic
- Ramadan period and related Islamic dates (tabular approximation)

The frontend (React + Vite + TypeScript) renders these events in an interactive calendar UI.

## Tech Stack

- **Frontend:** React, TypeScript, Vite, Zustand, TanStack Query, Axios
- **Backend:** FastAPI, Skyfield, NumPy, Pydantic, Uvicorn
- **Astronomy data:** `de421.bsp` (JPL/NASA ephemeris via Skyfield)

## Project Structure

- `Back/` - FastAPI app and calendar calculations
- `Front/` - React frontend
- `de421.bsp` - ephemeris file used for astronomical calculations
- `requirements.txt` - root requirements passthrough (`-r Back/requirements.txt`)

## Prerequisites

- Python 3.10+ recommended
- Node.js 18+ recommended
- npm

## Quick Start

### 1) Backend Setup

#### Windows (PowerShell)

```powershell
cd Back
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

#### macOS / Linux

```bash
cd Back
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

Backend runs at: [http://localhost:8000](http://localhost:8000)

### 2) Frontend Setup

Open a second terminal:

```bash
cd Front
npm install
npm run dev
```

Frontend runs at the Vite URL shown in terminal (typically [http://localhost:5173](http://localhost:5173)).

## Environment Configuration

Frontend optional variable:

```bash
VITE_API_BASE_URL=/api
```

By default in local development, Vite proxies `/api` requests to `http://localhost:8000`.

## API Overview

Main backend endpoints are defined in `Back/main.py` and provide calendar event data for requested date ranges and locations.

Typical event types include:
- `new_moon`
- `full_moon`
- `togool`
- `nooruz`
- `ramadan`
- `eid_al_fitr`
- `kadyr_tun`
- `ai_bashi`
- `kurman_ait`
- `holiday`

## Astronomy and Date Calculation Notes

- Astronomical computations are handled with Skyfield using `de421.bsp`.
- Timezone support uses IANA names (for example `Asia/Bishkek`).
- Islamic dates are computed using a tabular calendar approximation and may differ from moon-sighting-based local announcements.

## Troubleshooting

- **`de421.bsp` missing error:** ensure `de421.bsp` exists and is accessible to the backend.
- **Frontend cannot reach backend:** verify backend is running on port `8000`.
- **PowerShell execution policy issue:** run PowerShell as admin once and allow local script execution if needed.
- **Dependency install issues:** upgrade `pip`/`npm` and retry installation.

## Development Notes

- Backend dependencies: `Back/requirements.txt`
- Frontend dependencies: `Front/package.json`
- Root `requirements.txt` forwards to backend requirements for convenience.
