# Multi-Dimensional Quality Evaluation of Open-Source IDS/IPS Tools: Zeek, Snort 3, and Suricata

> MSc Cyber Security thesis — Aalborg University (2026). An independent, reproducible framework for comparing the three most widely deployed open-source intrusion detection systems across five quality dimensions.

![Focus](https://img.shields.io/badge/focus-IDS%2FIPS%20%7C%20SOC-1f3a66)
![Tools](https://img.shields.io/badge/tools-Snort%20%7C%20Suricata%20%7C%20Zeek-2e5aac)
![Dataset](https://img.shields.io/badge/dataset-CICIDS%202017%2F2018-555555)
![SIEM](https://img.shields.io/badge/SIEM-ELK%20Stack-005571)

---

## Overview

Organisations deploying open-source IDS/IPS tools face a real problem: there is no independent, multi-dimensional framework that compares **Zeek**, **Snort 3**, and **Suricata** in a structured, reproducible, and evidence-based way. Existing studies tend to evaluate a single dimension, exclude one of the tools, or rely on outdated datasets.

This project addresses that gap by designing and applying a **Quality Evaluation Framework (QEF)**, grounded in the **ISO/IEC 25010** software quality model, that evaluates all three tools simultaneously across five dimensions under identical controlled conditions using the modern **CICIDS 2017/2018** dataset.

## The five quality dimensions

| Dimension | What it measures | ISO 25010 mapping |
|---|---|---|
| **D1 — Detection Effectiveness** | True/false positive rate, attack coverage | Functional Suitability |
| **D2 — Performance Efficiency** | Throughput, CPU and memory usage | Performance Efficiency |
| **D3 — Resilience** | Detection degradation & packet drop under 2× load | Reliability |
| **D4 — Adaptability** | Custom rule/script support, anomaly detection, protocol coverage | Maintainability, Portability |
| **D5 — Interoperability** | Output format, SIEM integration, API/automation | Compatibility |

Each dimension is scored 1–5 using a defined scoring matrix, producing an average quality score per tool.

## Methodology (in brief)

- **Controlled lab:** a single Linux VM configured identically for all three tools, ensuring differences reflect the tools themselves rather than the environment.
- **Traffic replay:** the CICIDS 2017/2018 dataset (PCAP) was replayed with **tcpreplay** at normal (1×) and double (2×) speed.
- **Measurement:** alerts were compared against ground-truth labels using **Python** scripts to compute detection metrics; CPU/RAM were sampled during replay.
- **SIEM integration:** alerts were forwarded into the **ELK stack** (Elasticsearch, Logstash, Kibana) via Filebeat, and automation tooling (suricata-update, PulledPork, EVE JSON) was assessed.

## Key results

Average quality scores across the five dimensions:

| Tool | D1 | D2 | D3 | D4 | D5 | **Average** |
|---|---|---|---|---|---|---|
| **Zeek** | 4 | 4 | 5 | 4 | 4 | **4.20** |
| **Suricata** | 4 | 4 | 3 | 3 | 5 | **3.80** |
| **Snort 3** | 2 | 5 | 3 | 2 | 3 | **3.00** |

**Takeaways:**
- **Suricata** — highest detection rate and best interoperability; most SOC-ready where SIEM integration matters.
- **Zeek** — highest overall score, driven by resilience and adaptability; best suited to threat hunting and behavioural analysis.
- **Snort 3** — most resource-efficient, but its community rule set requires tuning before deployment.

*Note: Zeek was evaluated in its default logging configuration (without dedicated detection scripts) due to a plugin compatibility issue, which lowered its measured detection rate — a test-configuration limitation, not a capability ceiling. See the Limitations section of the thesis for full detail.*

## Repository structure

```
.
├── scripts/          # Python scripts: metric computation (TP/FP/TN/FN), CPU & memory analysis
├── results/          # Raw measurement data and scoring outputs
├── docs/             # Thesis PDF / supporting documentation
└── README.md
```


## Tools & technologies

`Snort 3` · `Suricata` · `Zeek` · `ELK Stack` · `tcpreplay` · `Wireshark` · `Python` · `Linux` · `CICIDS 2017/2018`

## Limitations

Testing was conducted in a virtualised environment with replayed (not live) traffic, results depend on the specific rule sets used, and a planned live-attack simulation (Nmap, Hydra, hping3) was not completed within the project scope. These are documented in full in the thesis.

## Author

**Khagendra Thakurathi** — MSc Cyber Security, Aalborg University
[LinkedIn](https://www.linkedin.com/in/khagendra-thakurathi-79341832b/) · thakurathikhagendra1997@gmail.com

*Co-authored with Mohamod Ansari.*

