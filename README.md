# 🏚️ Gaza Building Damage Assessment with DOFA & Maxar VHR Imagery

> **End-to-End GeoAI Pipeline for Conflict Damage Mapping using 50cm Satellite Imagery**

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python) ![PyTorch](https://img.shields.io/badge/PyTorch-Lightning-purple?logo=pytorch) ![Maxar](https://img.shields.io/badge/🛰️-Maxar_Open_Data-orange) ![Resolution](https://img.shields.io/badge/Resolution-50cm-red) ![Location](https://img.shields.io/badge/📍-Gaza_2023--2024-darkred)

---

## 🌍 What Is This Project?

This pipeline detects **building damage** from conflict using very high resolution (50cm) Maxar satellite imagery — the same imagery used by **UNOSAT**, **UN OCHA**, and **MSF** for operational humanitarian response.

It uses the **DOFA** foundation model to segment land cover in pre and post-event imagery, then classifies each area by damage severity:

| Class | Colour | Meaning |
|---|---|---|
| 🟢 No Damage | Green | Structure intact — same class before and after |
| 🟡 Minor Damage | Amber | Class changed slightly — possible structural stress |
| 🟠 Major Damage | Orange | Significant class change — partial collapse likely |
| 🔴 Destroyed | Red | Changed to bare soil / rubble — total loss |

---

## 🛰️ Data Source — Maxar Open Data Program

After major disasters, **Maxar Technologies** releases very high resolution imagery for free under their Open Data Program.

- **Resolution:** 50cm per pixel — individual buildings clearly visible
- **Coverage:** Gaza Strip, October 2023 (pre-event) and January 2024 (post-event)
- **License:** Creative Commons Attribution Non-Commercial 4.0
- **Access:** [maxar.com/open-data](https://www.maxar.com/open-data) — free, no account required

This is the same imagery used by:
- 🇺🇳 **UNOSAT** for UN damage assessments
- 🏥 **MSF** for operational field planning
- 🔴 **ICRC** for conflict zone mapping

---

## 📊 Results

### VHR Imagery Comparison
![VHR Comparison](outputs/damage/01_vhr_comparison.png)

### DOFA Segmentation
![Segmentation](outputs/damage/02_segmentation_comparison.png)

### Damage Map
![Damage Map](outputs/damage/03_damage_map.png)

### Damage Distribution
![Distribution](outputs/damage/04_damage_distribution.png)

### Chip Examples by Damage Class
![Examples](outputs/damage/05_chip_examples.png)

### Summary
![Summary](outputs/damage/06_summary_card.png)

---

## 🚀 How to Run

### 1. Clone the repo
```bash
git clone https://github.com/Bmaina/gaza-damage-assessment.git
cd gaza-damage-assessment
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run notebooks in order

| Notebook | What it does |
|---|---|
| `01_download_data.ipynb` | Downloads Maxar Open Data imagery. Falls back to synthetic demo data if unavailable. |
| `02_prepare_scenes.ipynb` | Normalises imagery, aligns pre/post scenes, chips into 64×64 DOFA patches |
| `03_assess_damage.ipynb` | Runs DOFA inference on all chips, classifies damage, reconstructs full-scene map |
| `04_visualise.ipynb` | Produces all 6 visualisation outputs |

> ⚠️ Update `CHECKPOINT_PATH` in `03_assess_damage.ipynb` to point to your DOFA checkpoint.

---

## 📁 Project Structure

```
gaza-damage-assessment/
├── 01_download_data.ipynb
├── 02_prepare_scenes.ipynb
├── 03_assess_damage.ipynb
├── 04_visualise.ipynb
├── data/
│   ├── raw/
│   │   ├── gaza_pre_event.tif    # Maxar pre-event (Oct 2023)
│   │   └── gaza_post_event.tif   # Maxar post-event (Jan 2024)
│   ├── prepared/
│   │   ├── pre_rgb.tif
│   │   ├── post_rgb.tif
│   │   └── chips_meta.json
│   └── chips/
│       ├── pre/                  # 64×64 pre-event patches
│       └── post/                 # 64×64 post-event patches
└── outputs/damage/
    ├── damage_map.tif
    ├── damage_results.csv
    └── 0*_*.png                  # Visualisations
```

---

## 🧠 Model

Uses **DOFA** (Dynamic One-For-All), a Vision Transformer pretrained on millions of satellite images. Fine-tuned on EuroSAT for land cover segmentation — applied here with no retraining.

**Key insight:** Damage manifests as land cover change. A residential block that becomes bare soil has been destroyed. DOFA detects this change at scale, automatically.

---

## 🌍 Real-World Applications

| Application | How This Pipeline Applies |
|---|---|
| ☮️ **Conflict Damage** | Map building destruction for humanitarian response prioritisation |
| 🌊 **Flood Response** | Detect inundated structures for rescue operations |
| 🔥 **Wildfire** | Map burned structures for insurance and recovery planning |
| 🌍 **Earthquake** | Assess collapse patterns for search and rescue |
| 💰 **Insurance** | Automated damage quantification for claims processing |

---

## 📚 References

- **DOFA Foundation Model** — [huggingface.co/earthflow/DOFA](https://huggingface.co/earthflow/DOFA)
- **Maxar Open Data** — [maxar.com/open-data](https://www.maxar.com/open-data)
- **UNOSAT Gaza Assessment** — [unosat.org](https://www.unosat.org)
- **geo-deep-learning** — [github.com/NRCan/geo-deep-learning](https://github.com/NRCan/geo-deep-learning)

---

<div align="center">
  <strong>Built by Benson M. Gachaga</strong><br/>
  Data Scientist | GeoAI Practitioner | Remote Sensing Specialist<br/><br/>
  <a href="https://linkedin.com/in/bensonmgachaga">LinkedIn</a> &nbsp;·&nbsp;
  <a href="https://github.com/Bmaina">GitHub</a>
</div>
