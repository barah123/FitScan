# FitScan

<p align="center">
  <img src="./www/app_logo.png" width="400" alt="FitScan logo" />
</p>

![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Built with R Shiny](https://img.shields.io/badge/built%20with-R%20Shiny-2a78d6)
![Python](https://img.shields.io/badge/python-reticulate-1baf7a)

---

**FitScan** is an R Shiny application that turns a raw **Google Health / Fitbit Takeout export** into a clean, explorable cardiovascular dashboard — no terminal required. It wraps Python-based extraction (via `reticulate`) and `ggplot2`-based visualization behind a single browser interface: upload a `.zip`, extract, and visualise, all in one place.

FitScan is designed to be:

- **Upload-driven** – accepts the standard Google Takeout `.zip` export directly, no manual unzipping or file wrangling.
- **Multi-participant** – load as many participants as you like into one session and unlock cross-participant comparison plots.
- **Exploration-ready** – a fixed cardiovascular dashboard for the essentials, plus an interactive explorer for any variable, chart type, and date range.
- **Fully downloadable** – every plot (and every extracted summary) can be downloaded individually or bundled as a zip.

---

## Installation

### Requirements

- R (≥ 4.1) with the following packages: `shiny`, `reticulate`, `ggplot2`, `dplyr`, `tidyr`, `scales`, `patchwork`, `DT`, `zip`
- Python 3 (FitScan provisions its own virtual environment automatically on first launch — no manual Python setup needed)

### From GitHub

```r
# install.packages("remotes")  # if needed
remotes::install_github("barah123/FitScan")
```

Or clone directly and run it as a project:

```bash
git clone https://github.com/barah123/FitScan.git
cd FitScan
```

```r
# From R, with the FitScan folder as the working directory
shiny::runApp(".")
```

The first launch takes a few extra seconds while `reticulate` builds a dedicated Python virtual environment (`r-fitbit-shiny`) with `pandas` installed. Every launch after that is instant.

---

## Input data format

FitScan expects the **Google Health Takeout `.zip`** exactly as downloaded from [Google Takeout](https://takeout.google.com/) for a Fitbit-linked Google Health account, unmodified. Internally it looks for the standard Takeout layout:

```
Takeout/Google Health/Physical Activity_GoogleData/
    daily_resting_heart_rate.csv
    daily_heart_rate_variability.csv
    steps_*.csv
    activity_level_*.csv
    active_zone_minutes_*.csv
    sedentary_period_*.csv
    heart_rate_*.csv
    daily_respiratory_rate.csv
Takeout/Google Health/Sleep Score/
    sleep_score.csv
```

Each `.csv` inside the zip is read and merged into one **daily summary per participant** — you do not need to extract or rename anything yourself; just upload the `.zip` as-is.

---

## App features

### 1. Upload & Manage
Upload a Takeout `.zip`, assign a participant ID (auto-suggested, editable), and extract its daily Fitbit summary in one click. Repeat for as many participants as needed — they all stay loaded for the session. Each participant's summary is downloadable as CSV, individually or bundled as a zip.

### 2. Participant Dashboard
A fixed, publication-style dashboard for one participant at a time: resting heart rate trend, heart rate range per day, daily steps, activity composition, active zone minutes, HRV across sleep nights, sedentary bouts, sleep quality, and a composite overview panel. Every plot has its own PNG download, plus a "download all" zip.

### 3. Explore
An interactive builder: pick any participant(s), any numeric variable (steps, HRV, sleep score, respiratory rate, and more), a chart type (line / bar / point), and a date range. Renders on the fly and downloads as PNG.

### 4. Compare Participants
Unlocks once 2+ participants are loaded: resting HR trend across participants, daily steps faceted by participant, resting HR distribution boxplot, and an HRV comparison plot — each downloadable individually or as a bundle.

---

## Example workflow

1. Open the app and go to **Upload & Manage**.
2. Upload `takeout-XXXXXXXXTXXXXXXZ-3-001.zip`, set the participant ID (e.g. `P01`), and click **Extract & add to session**.
3. Repeat step 2 for additional participants (e.g. `P02`, `P03`, …).
4. Go to **Participant Dashboard** to view the full cardiovascular dashboard for a chosen participant.
5. Go to **Explore** to build a custom view — pick a variable, chart type, and date range across one or more participants.
6. Once 2+ participants are loaded, go to **Compare Participants** for cross-participant plots.
7. Download any plot with its **Download PNG** button, or grab everything at once with a **Download all (zip)** button.

---

<table align="center">
  <tr>
    <td><img src="./www/scan1.png" width="420" /></td>
    <td><img src="./www/scan4.png" width="420" /></td>
  </tr>
  <tr>
    <td><img src="./www/scan2.png" width="420" /></td>
    <td><img src="./www/scan3.png" width="420" /></td>
  </tr>
</table>

---

## Contact

Developed by the **FITGut Lab** for research purposes.

📧 [fitgutlab@gwu.edu](mailto:fitgutlab@gwu.edu) · 📞 +1 202-994-2757 · [@fitgutlab](https://github.com/fitgutlab)

Department of Exercise and Nutrition Sciences · Milken Institute School of Public Health · George Washington University · Washington, DC, USA

---

![License: MIT](https://img.shields.io/badge/license-MIT-green)

Copyright (c) 2026 FITGut Lab, George Washington University

This project is licensed under the terms of the MIT license.
You are free to use, modify, and distribute this work, subject to the
conditions specified in the LICENSE file.
