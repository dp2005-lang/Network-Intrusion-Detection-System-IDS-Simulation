# Network-Intrusion-Detection-System-IDS-Simulation
A Network Intrusion Detection System (IDS) simulation that generates network traffic data, identifies suspicious patterns using machine learning, assigns risk scores, and provides an interactive dashboard for monitoring alerts, investigating incidents, and updating their status.
# 🛡️ Network Intrusion Detection System (IDS) Simulation

> **A defensive cybersecurity project that simulates network traffic, detects suspicious behavior using hybrid detection techniques, generates security alerts, correlates incidents, and visualizes results through a SOC-style dashboard.**

---

## 📌 Overview

The **Network Intrusion Detection System (IDS) Simulation** is an educational cybersecurity project designed to demonstrate how a modern intrusion detection workflow can identify potentially malicious network behavior.

The system operates entirely on **synthetic network-flow records**. It does not send packets, perform network scans, or interact with real networks.

The detection pipeline combines:

* Signature/rule-based detection
* Statistical anomaly detection
* Machine learning
* Hybrid risk scoring
* Alert generation and severity classification
* Alert correlation and incident grouping
* SQLite-based event storage
* SOC-style interactive dashboard
* Analyst status updates and investigation notes

---

## 🎯 Objectives

* Simulate realistic normal and suspicious network-flow patterns.
* Extract meaningful network security features from flow records.
* Detect suspicious behavior using configurable security rules.
* Apply supervised and unsupervised machine-learning techniques.
* Combine multiple detection layers into a single risk score.
* Generate actionable security alerts.
* Correlate related alerts into incidents.
* Provide an interactive dashboard for security monitoring.
* Demonstrate an end-to-end IDS/SOC workflow in Google Colab.

---

## 🔄 System Architecture

```text
Synthetic Network Traffic
          │
          ▼
   Feature Extraction
          │
          ├───────────────┐
          ▼               ▼
  Signature Rules   Anomaly Detection
          │               │
          └───────┬───────┘
                  ▼
          Machine Learning
                  │
                  ▼
           Hybrid Risk Score
                  │
                  ▼
          Alert Generation
                  │
                  ▼
          SQLite Event Store
                  │
          ┌───────┴────────┐
          ▼                ▼
 Alert Correlation    SOC Dashboard
          │                │
          └───────┬────────┘
                  ▼
          Incident Investigation
```

---

## 🔍 Detection Capabilities

The simulator generates both normal and suspicious traffic scenarios.

### Normal Traffic

* Web traffic
* DNS traffic
* SSH traffic
* Email traffic
* Database traffic

### Suspicious Traffic

* High connection rate
* Repeated failed connections
* Multi-port probing
* SYN-heavy behavior
* Unusual port activity
* High traffic volume

The system uses configurable thresholds to identify suspicious patterns.

---

## 🤖 Machine Learning

The project uses multiple machine-learning approaches to provide complementary detection capabilities.

### Supervised Learning

**Random Forest Classifier**

Used to classify network flows as normal or suspicious.

### Linear Model

**Logistic Regression**

Provides an additional supervised classification baseline.

### Unsupervised Learning

**Isolation Forest**

Learns the characteristics of normal traffic and identifies anomalous behavior.

### Evaluation Metrics

The trained models are evaluated using:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix

The dataset is divided into stratified training and testing sets, with the anomaly baseline learned from normal training flows.

---

## ⚡ Hybrid Risk Scoring

Instead of relying on a single detector, the IDS combines multiple signals.

With ML enabled, the default weighting is:

| Detection Layer   | Weight |
| ----------------- | -----: |
| Signature Rules   |    40% |
| Anomaly Detection |    30% |
| Machine Learning  |    30% |

When ML is disabled:

| Detection Layer   | Weight |
| ----------------- | -----: |
| Signature Rules   |    60% |
| Anomaly Detection |    40% |

The resulting **0–100 hybrid risk score** is used to prioritize alerts.

> A high risk score indicates that an event requires investigation; it is not treated as proof of malicious activity.

---

## 🚨 Alert Management

Generated alerts contain information such as:

* Alert ID
* Source IP
* Destination IP
* Source/Destination ports
* Protocol
* Alert type
* Severity
* Risk score
* Rule score
* Anomaly score
* ML score
* Matched detection rules
* Alert status
* Investigation information

### Alert Status Workflow

```text
NEW
 │
 ├──► INVESTIGATING
 │         │
 │         └──► RESOLVED
 │
 └──► FALSE_POSITIVE
```

The system validates status transitions to prevent invalid incident workflows.

---

## 🔗 Alert Correlation

Individual alerts can be correlated into larger incidents using a configurable time window.

This demonstrates how multiple related security events can be grouped together to help analysts identify broader attack patterns instead of investigating every alert independently.

---

## 🗄️ Data Storage

The project uses **SQLite** to store IDS events locally.

The database maintains information related to:

* Network flows
* Security alerts
* Detection rules
* Model results
* Incident notes

Indexes are also created for commonly queried alert and model-result fields.

---

## 🖥️ SOC Dashboard

The project generates a browser-based **Security Operations Center (SOC) dashboard**.

The dashboard provides visibility into:

* Total network flows
* Suspicious activity
* Security alerts
* Alert severity
* Risk scores
* Detection methods
* Incident information
* Model evaluation
* Analyst notes
* Investigation status

Analysts can update alert statuses and add investigation notes through the interface.

---

## 📊 Synthetic Dataset

The default simulation generates:

* **6,000 network-flow records**
* **4,800 normal flows**
* **1,200 suspicious flows**

The dataset contains multiple traffic scenarios designed specifically for demonstrating IDS detection techniques.

All addresses use documentation/test ranges, keeping the simulation isolated from real network infrastructure.

---

## 🧪 Testing

The notebook includes automated tests covering important IDS functionality, including:

* Normal-flow classification
* Feature extraction
* Configurable rule thresholds
* High connection-rate detection
* Repeated failed connections
* Multi-port activity
* SYN-heavy behavior
* High traffic volume
* Anomaly scoring
* Alert creation
* Alert correlation
* Status-transition validation
* Analyst notes
* Dashboard statistics
* Empty-dataset handling

---

## 📁 Generated Outputs

Running the notebook generates project artifacts such as:

```text
data/
└── network_traffic.csv

ids_events.db
ids_dashboard.html

dashboard_site/
└── index.html

reports/
├── incident_report.md
└── siem_alerts.jsonl
```

These outputs provide both structured security data and human-readable investigation reports.

---

## 🛠️ Technologies Used

* **Python**
* **Google Colab / Jupyter Notebook**
* **NumPy**
* **Pandas**
* **Scikit-learn**
* **SQLite**
* **IPython Widgets**
* **HTML/CSS/JavaScript**
* **JSON / JSONL**
* **Markdown**

---

## ▶️ How to Run

### Option 1 — Google Colab

1. Open the `.ipynb` file in Google Colab.
2. Run the single notebook cell.
3. Wait for dataset generation and model training.
4. Review the model evaluation results.
5. Explore generated IDS alerts.
6. Open the SOC dashboard from the displayed link.
7. Investigate alerts and update their status.

### Option 2 — Jupyter Notebook

Open the notebook using Jupyter Notebook or JupyterLab and execute the cell.

Required Python libraries include:

```bash
pip install numpy pandas scikit-learn ipywidgets
```

---

## ⚙️ Configuration

The IDS behavior can be customized through the `CONFIG` dictionary.

Examples of configurable parameters include:

```python
n_flows
suspicious_share
live_flows
use_ml
weights_ml
weights_no_ml
alert_min_risk
corr_window
window_seconds
```

Detection thresholds can also be adjusted for:

```text
Connection rate
Failed connections
Failure ratio
Unique destination ports
SYN count
SYN ratio
Traffic volume
```

---

## ⚠️ Security & Safety

This project is intentionally designed as a **defensive simulation**.

It:

* Does not capture real network packets.
* Does not scan networks.
* Does not send attack traffic.
* Does not interact with external systems.
* Uses synthetic flow records for all demonstrations.

It is therefore suitable for cybersecurity education, demonstrations, portfolio projects, and controlled experimentation.

---

## 📈 Limitations

The project uses synthetic traffic, so its machine-learning performance should not be interpreted as real-world IDS performance.

The detection rules are also designed around the simulated attack patterns. Consequently, model metrics can be significantly more optimistic than what would be expected on real enterprise network traffic.

For production deployment, the system would require:

* Real network telemetry
* Larger and more diverse datasets
* Continuous model validation
* Production-grade logging
* Authentication and authorization
* Secure data ingestion
* SIEM integration
* False-positive management
* Continuous monitoring and retraining

---

## 🚀 Future Enhancements

Potential extensions include:

* Real packet-flow ingestion in a controlled environment
* Deep-learning-based anomaly detection
* Real-time streaming pipelines
* Threat-intelligence integration
* MITRE ATT&CK mapping
* Automated incident-response playbooks
* Email/Slack security notifications
* Role-based analyst access
* Advanced visualization
* Model explainability using SHAP
* Integration with enterprise SIEM platforms

---

## 📚 Project Purpose

This project demonstrates the complete lifecycle of a simplified security monitoring system:

**Generate → Extract → Detect → Score → Alert → Correlate → Investigate → Report**

It is intended to provide practical understanding of how machine learning, statistical analysis, security rules, event storage, and SOC visualization can work together within an intrusion-detection workflow.

---

## 👩‍💻 Author

**Debankita Panja**

Cybersecurity / Machine Learning Project

---

## ⭐ Disclaimer

This project is intended strictly for **educational and defensive cybersecurity purposes**. All network activity represented by the system is synthetic and does not involve attacking, scanning, or monitoring real systems.
