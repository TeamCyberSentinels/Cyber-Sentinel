Here’s a suggested **GitHub repository structure** and a complete **README.md** for your project:

---

### 📁 Recommended Repository Structure

```
Cyber-Sentinel/
│
├── README.md
├── requirements.txt
│
├── code/
│   ├── securegpt_lambda_handler.py       # Code 1 - Multi-iteration NIST analysis
│   └── jira_ticketing_lambda.py          # Code 2 - Jira ticket automation
│
├── datasets/
│   ├── hdfs_logs_sample.csv
│   ├── server_logs_sample.csv
│   └── simulated_logs_sample.csv
│
└── docs/
    └── architecture_diagram.png          # Optional: Add architecture image if available
```

---

### 📄 README.md

```markdown
# 🛡️ Cyber Sentinel: AI-Powered NIST Compliance Monitoring

Cyber Sentinel is an intelligent agent-based system that automates the detection of non-compliant log entries based on NIST cybersecurity standards and auto-creates Jira tickets for high-priority violations. It leverages SecureGPT and AWS Lambda to perform a multi-iteration analysis workflow.

---

## 🧠 Project Overview

### Agent 1: NIST Compliance Monitoring (SecureGPT Integration)
- **Triggered by**: S3 object upload (logs)
- **Runs**: Three iterations (basic analysis → reflection → final validation)
- **Uses**: SecureGPT API to classify logs as compliant or non-compliant across NIST categories
- **Saves**: Results to `nistanomolies` S3 bucket under different folders per iteration

### Agent 2: Jira Ticketing Automation
- **Triggered by**: S3 uploads to `results/` folder
- **Parses**: Markdown tables of violations
- **Creates**: Jira tickets based on violation severity

---

## 📁 Repository Structure

```

cyber-sentinel-nist-ai/
├── code/
│   ├── securegpt\_lambda\_handler.py       # Main analysis pipeline
│   └── jira\_ticketing\_lambda.py          # Automated Jira ticket creation
├── datasets/
│   ├── hdfs\_logs\_sample.csv              # Real-world HDFS logs
│   ├── server\_logs\_sample.csv            # Security and system logs
│   └── simulated\_logs\_sample.csv         # Injected attack patterns for training
├── docs/
│   └── architecture\_diagram.png          # \[Optional] Workflow or architecture diagram
├── README.md
└── requirements.txt                      # Dependencies

````

---

## 📊 Datasets

| Dataset Name         | Source         | Purpose                                           |
|----------------------|----------------|---------------------------------------------------|
| `hdfs_logs_sample`   | Open Source    | System anomaly detection & failure prediction     |
| `server_logs_sample` | Open Source    | Cybersecurity compliance & threat detection       |
| `simulated_logs`     | Team-Generated | AI training with injected NIST attack patterns    |

---

## ⚙️ Requirements

- Python 3.8+
- `boto3`
- `requests`
- AWS Lambda
- Jira Cloud Access
- SecureGPT API access

To install dependencies:
```bash
pip install -r requirements.txt
````

---

## 🚀 Deployment

Each script is designed to run as an AWS Lambda function:

* `securegpt_lambda_handler.py` should be connected to an S3 trigger (on file upload).
* `jira_ticketing_lambda.py` should be triggered by uploads to a specific S3 path (e.g., `results/`).

---

## 🧪 Testing

* Use sample datasets under `/datasets` to simulate uploads to S3.
* Validate the output stored in the target S3 bucket (`nistanomolies`).
* Check Jira for automatically created tickets.

---

## 📜 License

This project is for educational and research purposes.

---
