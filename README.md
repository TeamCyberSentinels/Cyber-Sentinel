# 🛡️ Cyber Sentinel: Agentic AI for Real-Time NIST Compliance Monitoring

**Cyber Sentinel** is an agentic AI-based system built as part of the Secure AgenticAI initiative. It leverages advanced LLMs (SecureGPT), prompt engineering techniques (Chain-of-Thought and Reflexion), and cloud-native infrastructure (AWS Lambda, S3, Jira) to perform real-time log compliance analysis aligned with NIST cybersecurity standards.

---

## 🚀 Problem Statement

Modern organizations face significant challenges in adhering to NIST compliance due to:
- High volumes of unstructured logs
- Manual, error-prone audits
- Delayed detection of violations

**Cyber Sentinel** solves this by using agentic AI to:
- Ingest logs from AWS S3
- Classify log lines as compliant or non-compliant
- Trigger remediation actions by automatically generating Jira service tickets

---

## 🧠 Solution Architecture

The system consists of two Lambda-based AI agents:

### 🔹 Agent 1: Compliance Monitoring Agent
- Triggered by log upload to `tcslogbucket`
- Uses **SecureGPT** to classify logs via a 3-iteration reasoning cycle:
  1. Initial NIST-based classification
  2. Reflexive severity assignment
  3. Final validation against ground-truth rules
- Stores results in `nistanomolies` S3 bucket

### 🔹 Agent 2: Jira Ticketing Agent
- Triggered by new compliance results in S3 under `results/`
- Parses violations and auto-creates Jira tasks
- Includes fields like `log_line`, `NIST control`, `severity`, and `description`

---

## 🧱 System Diagram

```
Logs (HDFS / Simulated / Server Logs) --> S3 Upload --> Agent 1 (Lambda) --> SecureGPT Iterative Analysis --> S3 Storage (Structured JSON)
|
Trigger --> Agent 2 (Lambda) --> Jira Ticket Creation
```

---

## 🗂️ Repository Structure

```bash
cyber-sentinel-nist-ai/
├── README.md
├── requirements.txt
├── code/
│   ├── securegpt_lambda_handler.py       # Agent 1 - NIST analysis
│   └── jira_ticketing_lambda.py          # Agent 2 - Jira integration
├── datasets/
│   ├── hdfs_logs_sample.csv              # Real-world logs
│   ├── server_logs_sample.csv            # Simulated logs
│   └── simulated_logs_sample.csv         # AI-generated logs
├── docs/
│   └── System Overview.png
│   ├── Sentinel Workflow            
```

---

## 📊 Datasets Used

| Dataset                     | Type         | Source            | Purpose                                |
| --------------------------- | ------------ | ----------------- | -------------------------------------- |
| `hdfs_logs_sample.csv`      | Real-world   | Loghub - LLNL     | Anomaly detection, fault prediction    |
| `server_logs_sample.csv`    | Synthetic    | Team-generated    | Policy testing, NIST validation        |
| `simulated_logs_sample.csv` | AI-generated | SecureGPT prompts | Training LLMs on structured violations |

Each log entry is evaluated against NIST SP 800-53, SP 800-92, and SP 800-171 rules using structured prompts and validated through 3-phase iteration.

---

## ⚙️ Tech Stack

* **AWS Lambda**: Event-based compute for agent logic
* **Amazon S3**: Log storage and pipeline state management
* **SecureGPT API**: Multi-step prompt-based classification
* **Jira Cloud API**: Auto-ticket creation for violations
* **Python 3.8+**
* **Prompt Engineering**: Chain-of-Thought + Reflexion

---

## 📦 Installation

Install dependencies locally:

```bash
pip install -r requirements.txt
```

`requirements.txt`:

```
boto3==1.34.76
requests==2.31.0
urllib3==1.26.18
```

---

## 🧪 Testing & Results

* Total logs processed: **17,000+**
* Accuracy across test cases: **85–95%**
* Average F1 Score: **91.4%**
* Recall: **Excellent**, especially for high-severity violations
* Ticket generation latency: **<5 seconds** per violation

---

## 🧩 How It Works

### Lambda 1: `securegpt_lambda_handler.py`

* Trigger: S3 upload
* Steps:

  1. Upload log to SecureGPT
  2. Analyze in 3 iterations
  3. Save JSON results to S3
  4. Trigger next iteration or Agent 2

### Lambda 2: `jira_ticketing_lambda.py`

* Trigger: New file in `nistanomolies/results/`
* Steps:

  1. Read structured violations from JSON
  2. Parse Markdown tables
  3. Create Jira tickets using REST API
  4. Return summary of generated tasks

---

## 🔒 Security & Privacy

* AWS S3: Encrypted logs with IAM access control
* Jira credentials stored in **AWS Secrets Manager**
* SecureGPT requests authenticated with **Bearer Token**
* Full audit trails via CloudWatch Logs

---

## 📈 Impact & Future Work

### Benefits

* Automates compliance workflows (Identify → Detect → Respond)
* Frees security teams from manual log review
* Enables real-time risk mitigation
* Reduces regulatory fines and operational delays

### Future Enhancements

* Support for HIPAA, ISO 27001 frameworks
* Self-healing integrations (e.g., revert misconfigurations)
* Real-time dashboards via AWS QuickSight or Streamlit
* GitHub Actions for CI/CD testing of Lambda code

---

## 🙌 Contributors

**Team Cyber Sentinel – DAEN 690, Spring 2025**

* Harinipriya Vasu
* Atharva Shrikhande
* David Jampana Abraham Luther
* Deeksha Abbadasari
* Kishore Karanam
* Pavan Kumar Ravuri
* * Sathwik Reddy Bethi

---

## 📜 License

This project is part of George Mason University's DAEN Capstone and is intended for educational and demonstration purposes only.

---
