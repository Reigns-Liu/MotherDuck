# MotherDuck

A small Streamlit demo that uses DuckDB with a MotherDuck (managed DuckDB) connection.

This project provides a simple web UI to register auction participants, record bids, and perform basic admin actions (search, view totals, and delete data).

**Notes:** The repository currently contains example tokens in source files. Remove any hard-coded tokens and use environment variables before deploying.

## Features

- Participant registration (ID, name, phone) via `app.py`.
- Simple bidding table and aggregation (`bids` table).
- Admin dashboard with search, totals, and delete capabilities.
- Example helper script: `MotherDuck.py` (demo for querying the DB).

## Files

- `app.py`: Streamlit application and primary UI.
- `MotherDuck.py`: Lightweight script demonstrating a DuckDB query against the same `TestDB`.
- `requirements.txt`: Python dependency list.

## Requirements

- Python 3.8+ (recommend 3.10+)
- `pip` and virtual environment utilities

## Installation

1. Create and activate a virtual environment (PowerShell):

```powershell
python -m venv .venv; .\.venv\Scripts\Activate.ps1
```

2. Install dependencies:

```powershell
pip install -r requirements.txt
```

## Configuration

- The code currently expects a MotherDuck token to connect to a managed DuckDB instance.
- Instead of keeping the token in source, set an environment variable and update the code to read it. Example (PowerShell):

```powershell
$env:MOTHERDUCK_TOKEN = 'your_token_here'
```

Then update `app.py`/`MotherDuck.py` to use the environment variable, e.g.:

```python
import os
motherduck_token = os.environ.get('MOTHERDUCK_TOKEN')
con = duckdb.connect(f"md:TestDB?motherduck_token={motherduck_token}")
```

## Running

Start the Streamlit app:

```powershell
streamlit run app.py
```

Open the URL printed by Streamlit in your browser.

## Database schema (created automatically)

- `roster` (id TEXT PRIMARY KEY, name TEXT, phone TEXT)
- `bids` (id TEXT, item_id TEXT, bid INT)

## Default credentials and security

- The Streamlit app uses a hard-coded demo password `1234567` for admin actions. Change this before any real use.
- Remove hard-coded tokens and passwords from source control. Use environment variables or a secrets manager.