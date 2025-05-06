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



