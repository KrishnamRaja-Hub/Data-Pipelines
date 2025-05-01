# Data-Pipelines

# Agent Performance Data Pipeline

This project builds a data processing pipeline to analyze and summarize the daily performance of customer support agents across calls, logins, and outcomes. It merges multiple data sources, computes agent-level metrics, and generates a daily performance summary report.

## 📌 Objective

To automate the process of reading raw agent call and login data, validate and transform the datasets, engineer performance metrics, and generate a clean summary CSV along with a human-readable Slack-style performance message.

## 📂 Data Sources

The pipeline ingests data from 3 CSV files:
- `call_data.csv` – Contains details about outbound calls (agent ID, organization ID, timestamps, and outcome).
- `login_data.csv` – Tracks login sessions of agents (login and logout times).
- `agent_info.csv` – Maps agent IDs to names.

## ⚙️ Features

- **Data Validation**: Ensures required fields like `call_date`, `agent_id`, and `org_id` exist and flags missing or duplicate records.
- **Robust Joins**: Merges call, login, and agent info data on `agent_id`, `org_id`, and `call_date`, while handling mismatches gracefully.
- **Feature Engineering**: Computes key agent metrics:
  - `Total Calls Made`
  - `Unique Loans Contacted`
  - `Connect Rate` = Completed Calls / Total Calls
  - `Average Call Duration` (in minutes)
  - `Presence` (1 if login info available, else 0)
- **Slack-style Summary Generation**: Produces a daily summary with:
  - Top performer (highest connect rate)
  - Total active agents
  - Average call duration
- **Output**:
  - Saves `agent_performance_summary.csv`
  - Prints formatted performance summary

## 💡 Example Output
Agent Summary for 2025-04-28
Top Performer: Ravi Sharma (98% connect rate)
Total Active Agents: 45
Average Duration: 6.5 min

## 🛠️ Technologies Used

- Python (pandas, argparse)
- Logging for debugging and traceability
- Modularized with functions for readability and testing
- CLI support for flexible file input

## 🚀 How to Run
Head over to the following google colab link: https://colab.research.google.com/drive/1vd0H9NVLB0ZK4xPA1MJgHlwpEtUW5IX0

OR

```bash
python main.py --calls_file call_data.csv --logins_file login_data.csv --agent_file agent_info.csv

