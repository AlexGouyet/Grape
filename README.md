# Grape.ag — Powdery Mildew Risk Algorithm 🍇

**[![Download on the App Store](https://img.shields.io/badge/Download_on_the-App_Store-black?logo=apple&style=for-the-badge)](https://apps.apple.com/us/app/grape-ag/id1525749253)**

*UC Davis published the Powdery Mildew risk model in the 1960s. Grape.ag was the first platform to implement it at per-vine resolution using modern IoT sensor networks. This repo contains v1 of the prediction algorithm I prototyped during my viticulture engineering internship at Grape.ag.*

<!-- HERO IMAGE: drop a Grape.ag app screenshot or vineyard shot here -->
<!-- ![Grape.ag hero](assets/hero.png) -->

---

## What Grape.ag Is

Grape.ag is a data-driven agriculture platform for vineyards, shipped to the App Store and actively maintained (currently v2.1.0, Feb 2026). It turns soil and atmospheric sensor data into real-time, actionable decisions for grape growers:

- Activity logs with voice notes per crop activity
- Growing Degree Day (GDD) charts and growth cycle tracking
- Soil moisture + temperature monitoring across multiple fields
- 7-day weather forecasting and wind direction analytics
- **Powdery Mildew (PM) risk index** computed per sensor block ← this repo

---

## My Contribution

I interned at Grape.ag from August 2020 to April 2021 as a Viticulture Engineering Intern. Key contributions:

- **Implemented the UC Davis PM risk algorithm in Python** — turned decades-old academic research into a production Python script. The script ran every 15 minutes on AWS Lambda, ingesting live sensor data and populating the React Native app that vineyard owners carried in the field.
- **Global market analysis** — identified new agricultural opportunities in Southern Mexico, contributing ~15% revenue growth
- **Crop protection impact** — predictive algorithms contributed to a **20% improvement in crop protection efficiency**

---

## The Algorithm

The PM risk model comes from UC Davis research originally published in the 1960s. The rule is elegant but historically expensive to compute at field scale:

> Powdery Mildew risk is elevated when **daily mean temperature > 10°C** AND **mean relative humidity has been > 85% for 10 consecutive days**.

For decades this was computed regionally using weather stations. Computing it *per vine block* — via cheap in-field IoT sensors — only became feasible when sensor and cloud-compute costs collapsed 60 years later.

The notebook implements v1 of that rule:

1. Ingest raw sensor readings (timestamp, temp, humidity, sensor_id) from CSV exports
2. Bucket into daily windows per sensor using pandas groupby
3. Compute daily mean temperature → flag if > 10°C
4. Compute rolling 10-day mean humidity → flag if > 85%
5. Join conditions into a per-sensor, per-day risk table

**Stack:** Python · pandas · datetime · AWS Lambda (cron-triggered every 15 minutes) · React Native (field-facing app)

---

## Repo Contents

| File | What it is |
|------|-----------|
| `Grape PM Algo #1.ipynb` | Jupyter notebook — v1 of the Powdery Mildew risk algorithm |

This repo is a snapshot of early algorithm work. The production system went through many iterations and improvements by the Grape.ag team after I left.

---

## Links

- 📱 [Grape.ag on the App Store](https://apps.apple.com/us/app/grape-ag/id1525749253)
- 🌐 [grape.ag](https://grape.ag)

---

*Built during my viticulture engineering internship at Grape.ag, 2020–2021. The team and the app are still going strong in 2026.*
