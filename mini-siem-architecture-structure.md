# Mini SIEM Architecture & Directory Structure

## 1. Project Architecture

This mini SIEM operates on a **Modular Pipeline** architecture. Instead of one large script, we divide tasks into specialized "engines."

1.  **Ingestion (Log Parser):** Takes raw log files (CSV, Apache Access, Auth logs), cleans the data, and converts it into a structured format (Pandas DataFrame).
2.  **Analysis (Detection Engine):** Scans the structured data against pre-defined security rules (Brute-force, 404 spikes, etc.) to find anomalies.
3.  **Alerting (Alert Manager):** When the Detection Engine finds a match, the Alert Manager creates a formal "Alert" object with a severity level and status.
4.  **Visualization (Streamlit App):** The dashboard calls these modules, displays charts (Plotly), and provides the user interface for filters and exports.
5.  **Reporting (Report Generator):** Summarizes the findings into a downloadable format.

---

## 2. Directory Structure

This structure follows professional software development practices, separating logic (`modules/`), data (`data/`), and testing (`tests/`).

```text
mini-siem-log-analyzer/
│
├── app.py                      # Main entry point (Streamlit UI)
├── requirements.txt            # Project dependencies
├── README.md                   # Project documentation
├── .gitignore                  # Files Git should ignore
│
├── modules/
│   ├── __init__.py             # Makes folder a Python package
│   ├── log_parser.py           # Logic to read and clean logs
│   ├── detection_engine.py     # Security rules and logic
│   ├── alert_manager.py        # Managing and filtering alerts
│   ├── report_generator.py     # Creating CSV/Text exports
│   └── sample_log_generator.py # Script to create fake test data
│
├── data/                       # Stores sample logs (Generated)
│   ├── sample_auth.log
│   └── sample_access.log
│
└── tests/                      # Automated tests
    ├── test_log_parser.py
    └── test_detection_engine.py
```

---

## 3. Technology Stack Roles

*   **Python:** The "glue" that connects every module.
*   **Pandas:** The "data engine" that filters thousands of log lines in milliseconds.
*   **Streamlit:** The "front-end" that turns Python scripts into a web dashboard.
*   **Plotly:** The "artist" that creates interactive, clickable charts.
