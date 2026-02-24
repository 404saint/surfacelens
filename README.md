# SurfaceLens

![Python](https://img.shields.io/badge/language-python-3776AB?logo=python\&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active%20development-blue)
![Security Research](https://img.shields.io/badge/use--case-passive%20recon-critical)
![Shadow IT](https://img.shields.io/badge/feature-shadow%20IT-orange)

**SurfaceLens** is a **passive attack surface and Shadow IT intelligence engine**, designed to help security teams understand **what is exposed**, **why it matters**, and **how risky it is**, without performing active scanning.

It supports **two execution modes**:

* **Online** — live Shodan API
* **Offline** — user-supplied JSON datasets

Both modes feed the same **analysis pipeline**, producing **explainable risk scores**, **Shadow IT indicators**, and **professional reports**.

---

## Architecture Overview

<p align="center">
  <img src="example/surfacelens-architecture.svg" alt="SurfaceLens execution flow diagram" width="300">
</p>

---

## Architecture Explanation

SurfaceLens follows a **source-agnostic, passive analysis pipeline**:

### 1. Mode Selection

Users choose between:

* **Online Mode** — fetch assets via Shodan API
* **Offline Mode** — load JSON datasets

Invalid selections or load failures exit gracefully.


### 2. Asset Deduplication

Duplicates are removed based on **IP and port**, recording **first/last seen timestamps** for timeline insights.


### 3. Asset Analysis Pipeline

Each asset undergoes:

1. **Service Categorization** — e.g., remote access, admin panel, database
2. **Exposure Analysis** — high-risk ports, missing TLS
3. **Shadow IT Detection** — hostname and certificate mismatches
4. **Risk Scoring** — numeric score (0–10) with confidence based on service type, exposure, and Shadow IT signals

This ensures **consistent, explainable evaluation**.


### 4. Report Generation

After analysis, reports can be generated in:

* **JSON** — structured, machine-readable
* **Markdown** — human-readable for audits
* **HTML** — executive-friendly, formatted

Reports are timestamped and saved to the current directory.

---

## Capabilities

* Online mode (live Shodan API)
* Offline mode (JSON datasets)
* Passive asset discovery (no active scanning)
* Shadow IT detection with confidence scoring
* Explainable risk scoring for each asset
* Deduplication with first/last seen tracking
* Multi-format report generation (JSON, Markdown, HTML)

---

## Installation

```bash
git clone https://github.com/404saint/surfacelens.git
cd surfacelens
pip install shodan
```

> Python 3.9+ recommended.

### Optional — Online Mode

Set your **Shodan API key** for online analysis:

```bash
export SHODAN_API_KEY="YOUR_API_KEY"
```

Offline mode works without Shodan.

---

## Usage

```bash
python surfacelens.py
```

Follow the interactive prompts:

1. **Select mode** — Online or Offline
2. **Provide organization or ASN** (for Online) or **JSON file path** (for Offline)
3. **Analyze assets** — deduplication, exposure, Shadow IT, risk scoring
4. **Generate report** — choose JSON, Markdown, or HTML

---

## Example Output (Per Asset)

* Service category
* Exposure findings
* Shadow IT indicators (with confidence)
* Risk score (0–10) and confidence
* Explanation of risk factors

Reports are suitable for **technical teams**, **leadership**, and **audit documentation**.

---

## Ethical Use & Non-Goals

SurfaceLens is strictly **passive and defensive**:

* No active scanning
* No exploitation or brute forcing
* Only analyze assets you own or are authorized to assess

---

## License

MIT License
