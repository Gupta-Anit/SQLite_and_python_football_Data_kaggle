# European Soccer Database — SQLite & Python Analysis

Analytical exploration of the Kaggle **European Soccer Database** using SQL queries executed against a SQLite database from Python (`sqlite3` + `pandas`). The notebook answers a set of analytical questions about players, leagues, teams, and match goals, returning each result as a tidy pandas `DataFrame`.

## Overview

The project connects to the bundled SQLite database with Python's standard-library `sqlite3` driver and runs SQL queries through `pandas.read_sql_query`, materializing the results as DataFrames for inspection. The analyses cover:

1. **Players by age** — list all players born between 1987 and 1990 (inclusive), ordered oldest to youngest.
2. **Goals by country & league** — rank countries/leagues by total goals scored across the dataset, descending.
3. **Team strength by team attributes** — rank teams by the average of their team-level attributes (build-up play, defence, chance creation, etc.), best to worst.
4. **Top teams by attribute average** — the top 5 teams ranked by their averaged attributes.
5. **Highest-scoring date per season & league** — a single SQL query finding the date with the most goals scored, per season per league.
6. **Top scorers per league (2008/2009)** — a single windowed SQL query ranking the top 5 goal-scoring teams per league for the 2008/2009 season, combining home and away goals with `UNION ALL` and `ROW_NUMBER() OVER (PARTITION BY ...)`.

## Data

- **Source:** [European Soccer Database (Kaggle)](https://www.kaggle.com/datasets/hugomathien/soccer)
- **Format:** A single SQLite file (`database.sqlite`) containing tables including `Player`, `Match`, `Country`, `League`, `Team`, and `Team_Attributes`.
- **Note:** The `.sqlite` database is **not bundled** in this repository (it is large and excluded via `.gitignore`). Download it from Kaggle and place `database.sqlite` in the repository root before running the notebook.

## Approach

- Establish a connection with `sqlite3.connect('database.sqlite')`.
- Express each analytical question as a SQL query (joins across `Match`, `Country`, `League`, `Team`, `Team_Attributes`, `Player`).
- Execute queries with `pandas.read_sql_query(...)`, returning DataFrames.
- Techniques used include multi-table joins, aggregation (`SUM`, `AVG`), `GROUP BY`/`ORDER BY`, date handling (`strftime`, `substr`), `IFNULL`, `UNION ALL`, and the `ROW_NUMBER() OVER (PARTITION BY ...)` window function for per-league ranking.

## Repository structure

| File | Purpose |
|------|---------|
| `european_soccer_sqlite_analysis.ipynb` | Jupyter notebook with the SQL queries and pandas analysis |
| `requirements.txt` | Python dependencies |
| `.gitignore` | Ignored files (checkpoints, caches, the `.sqlite` data file, env files) |
| `LICENSE` | MIT license |
| `README.md` | This document |

## Tech stack

- **Python 3**
- **SQLite** (via the standard-library `sqlite3` module)
- **pandas** for query execution and result handling
- **Jupyter Notebook** as the analysis environment

## Setup & usage

```bash
# 1. (Optional) create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Download the European Soccer Database from Kaggle and place
#    database.sqlite in the repository root:
#    https://www.kaggle.com/datasets/hugomathien/soccer

# 4. Launch Jupyter and open the notebook
jupyter notebook european_soccer_sqlite_analysis.ipynb
```

## License

Released under the [MIT License](LICENSE).
