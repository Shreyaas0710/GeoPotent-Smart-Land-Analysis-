<div align="center">

<h1>🌍 GeoPotent</h1>
<h3>Smart Land Analysis Platform</h3>
<p><em>Solar &nbsp;·&nbsp; Wind &nbsp;·&nbsp; Soil &nbsp;·&nbsp; Agri Intelligence</em></p>

<br/>

<p>
  <img src="https://img.shields.io/badge/Django-4.x-092E20?style=for-the-badge&logo=django&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white"/>
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Deployed-Render-46E3B7?style=for-the-badge&logo=render&logoColor=black"/>
  <img src="https://img.shields.io/badge/Vercel-Ready-000000?style=for-the-badge&logo=vercel&logoColor=white"/>
</p>

<p>
  <img src="https://img.shields.io/badge/Status-Active-22c55e?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/APIs-SoilGrids%20%7C%20Open--Meteo-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/PDF-xhtml2pdf-red?style=flat-square"/>
</p>

<br/>

> **GeoPotent** is a full-stack Django web platform that analyses any GPS coordinate for its **solar energy**, **wind energy**, **soil quality**, and **agricultural revenue** potential — and connects landowners with solar plant builders through a built-in marketplace and proposal system.

<br/>

</div>

---

## ✦ What Is This?

Most landowners don't know what their land is truly worth — energetically or agriculturally.

**GeoPotent** changes that. Enter any latitude/longitude, set your land area and date range, and the platform:

- Queries **real-time soil data** from the SoilGrids API (pH, clay, sand, nitrogen, SOC)
- Pulls **historical weather** from the Open-Meteo Archive (hourly solar irradiance + wind speed)
- Models **PV solar** and **wind turbine** energy output with configurable hardware parameters
- Recommends **optimal crops** based on soil type and estimates agricultural revenue
- Computes a **mixed land-use strategy** comparing pure energy vs. agri-energy hybrid approaches
- Generates a **downloadable PDF report** with charts, projections, and soil breakdowns
- Connects landowners to **PV plant builders** via a proposal & negotiation marketplace

---

## ⚡ Feature Highlights

```
🌞 Solar PV Analysis       →  Configurable efficiency, coverage ratio, performance factor
💨 Wind Energy Modelling   →  Rotor diameter, hub height, cut-in/cut-out speeds, power curve
🪱 Soil Intelligence       →  SoilGrids API: pH, clay %, sand %, nitrogen, SOC at 3 depths
🌾 Crop Recommendations    →  Soil-type-matched crops with yield & revenue per hectare (₹)
⚡ Mixed Potential Score   →  Side-by-side: pure energy vs. agri-energy hybrid strategy
📄 PDF Report Export       →  Full report with embedded Matplotlib charts via xhtml2pdf
🤝 Builder Marketplace     →  Browse solar builders, submit proposals, negotiate deals
📜 Legal Bond System       →  Finalized deals generate a bond document between parties
👤 Dual Role Auth          →  Separate signup flows for Landowners and PV Plant Builders
🗺️  Land Registry          →  Landowners register multiple plots with GPS coordinates
```

---

## 🗂️ Project Structure

```
GeoPotent/
│
├── geopotent/                       # Django project config
│   ├── settings.py                  # Env-based config (django-environ)
│   ├── urls.py                      # Root URL dispatcher
│   ├── wsgi.py / asgi.py
│
├── potential_app/                   # Core application
│   ├── models.py                    # UserProfile, BuilderProfile, Land,
│   │                                #   LandAnalysis, Proposal, Bond
│   ├── views.py                     # Analysis pipeline: input → process → results → report
│   ├── views_auth.py                # Signup (landowner + builder), login, logout
│   ├── views_business.py            # Dashboard, AddLand, BuilderList,
│   │                                #   SubmitProposal, ProposalDetail
│   ├── urls.py                      # All URL routes
│   ├── forms.py                     # LandAnalysisForm, AdvancedSettingsForm,
│   │                                #   LandForm, ProposalForm
│   ├── allauth_adapter.py           # Custom allauth adapter
│   ├── templatetags/
│   │   └── custom_filters.py        # Custom template filters
│   └── templates/potential_app/
│       ├── index.html               # Landing page
│       ├── input_form.html          # Analysis input + advanced settings
│       ├── results.html             # Full results dashboard
│       ├── report_template.html     # Printable / PDF report
│       ├── dashboard_landowner.html
│       ├── dashboard_builder.html
│       ├── builder_list.html
│       ├── submit_proposal.html
│       ├── proposal_detail.html
│       ├── add_land.html
│       ├── login.html / signup.html / signup_builder.html
│       └── base.html
│
├── utils/
│   ├── soil_analysis.py             # SoilGrids API + crop recommendation engine
│   └── energy_estimation.py         # Open-Meteo weather + PV/Wind energy modelling
│
├── static/css/main.css
├── staticfiles/                     # Collected statics (production)
├── db.sqlite3                       # Default SQLite database
├── Procfile                         # Render/Heroku (gunicorn)
├── vercel.json                      # Vercel serverless config
└── manage.py
```

---

## 🧠 Analysis Engine

### 🌞 PV Solar Model

| Parameter | Default | Description |
|---|---|---|
| `pv_efficiency` | 0.20 (20%) | Panel conversion efficiency |
| `pv_performance_ratio` | 0.80 | Real-world losses factor |
| `pv_land_coverage` | 0.60 | Fraction of land covered by panels |
| `pv_system_efficiency` | 0.95 | Inverter and wiring efficiency |

> `Energy (kWh) = GHI (W/m²) × Area × Coverage × Efficiency × PR × System_eff`

### 💨 Wind Turbine Model

| Parameter | Default | Description |
|---|---|---|
| `wind_rated_power_kw` | 5.0 kW | Rated output power |
| `wind_rotor_diameter_m` | 7.0 m | Rotor swept area diameter |
| `wind_hub_height_m` | 20.0 m | Hub height for wind shear correction |
| `wind_cut_in_ms` | 3.0 m/s | Minimum operational wind speed |
| `wind_rated_ws_ms` | 12.0 m/s | Wind speed at rated power |
| `wind_cut_out_ms` | 25.0 m/s | Safety shutdown speed |
| `wind_alpha` | 0.14 | Wind shear exponent (terrain roughness) |

### 🪱 Soil Analysis

Fetches **5 properties** at **3 depth layers** (0–5 cm, 5–15 cm, 15–30 cm) via the SoilGrids REST API:

`phh2o` · `clay` · `sand` · `soc` (organic carbon) · `nitrogen`

Crops are matched against pH, clay %, sand %, and SOC thresholds from a curated crop database with yield (kg/ha) and market price (₹/kg).

---

## 🗄️ Data Models

### `UserProfile` — Role Extension
Linked to Django's `User` model (OneToOne). Role: `landowner` or `builder`.

### `BuilderProfile` — Solar Company
Company name, description, experience years, portfolio images (JSON list of URLs), customer reviews (JSON).

### `Land` — Registered Plot
GPS coordinates (lat/lon), area in m², address, and proof document upload.

### `LandAnalysis` — Analysis Record
Full input configuration (PV params, wind params, date range, area, coordinates) and all computed outputs stored as JSON: `soil_data`, `crop_recommendations`, `energy_results`.

### `Proposal` — Marketplace Deal
Links landowner → builder via a `LandAnalysis`. Status lifecycle:

```
pending_builder  →  accepted / rejected  →  negotiating  →  finalized
```

Investment model: `self_invest` (landowner owns system) or `builder_invest` (lease/transfer).

### `Bond` — Legal Agreement
Auto-generated on deal finalization. Stores bond text, signed timestamp, and active flag.

---

## 🛣️ URL Routes

| Route | View | Auth | Description |
|---|---|---|---|
| `/` | `IndexView` | Public | Landing page |
| `/analyze/` | `AnalysisInputView` | Public | Land analysis input form |
| `/process/<id>/` | `ProcessAnalysisView` | Public | Runs the full analysis pipeline |
| `/results/<id>/` | `ResultsView` | Public | Interactive results dashboard |
| `/report/<id>/` | `ReportView` | Public | Browser-rendered report |
| `/report-download/<id>/` | `ReportDownloadView` | Public | Download PDF report |
| `/builders/` | `BuilderListView` | Public | Browse registered solar builders |
| `/builders/<id>/submit/` | `SubmitProposalView` | Login | Send proposal to a builder |
| `/dashboard/` | `DashboardView` | Login | Landowner / Builder dashboard |
| `/dashboard/add-land/` | `AddLandView` | Login | Register a new land plot |
| `/proposals/<id>/` | `ProposalDetailView` | Login | View & respond to a proposal |
| `/signup/` | `signup_view` | Public | Landowner registration |
| `/signup-builder/` | `builder_signup_view` | Public | Builder registration |
| `/login/` · `/logout/` | Auth views | — | Session authentication |

---

## 🔄 Analysis Pipeline

```
  User submits coordinates + date range + PV/Wind config
                      │
                      ▼
          AnalysisInputView (POST)
          Saves LandAnalysis → redirects to /process/
                      │
                      ▼
          ProcessAnalysisView
          ├── get_soil_data()            ←  SoilGrids REST API
          ├── recommend_crops()          ←  Soil-matched crop logic
          ├── estimate_energy_potential()
          │   ├── fetch_hourly_weather() ←  Open-Meteo Archive API
          │   ├── PV energy per hour     ←  GHI × area × config params
          │   └── Wind energy per hour   ←  Power curve model
          ├── estimate_agri_revenue()    ←  Yield × price × area_ha (₹)
          ├── calculate_mixed_potential() ← Hybrid strategy scoring
          └── Saves JSON results → LandAnalysis.energy_results
                      │
                      ▼
          ResultsView  →  results.html (charts, tables, recommendations)
                      │
                      ▼
          ReportDownloadView
          ├── Renders 2×2 Matplotlib chart grid
          └── xhtml2pdf → PDF attachment download
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- Git

### 1 — Clone the Repository

```bash
git clone https://github.com/your-username/GeoPotent-Smart-Land-Analysis.git
cd GeoPotent-Smart-Land-Analysis
```

### 2 — Set Up Virtual Environment

```bash
python -m venv venv

source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows
```

### 3 — Install Dependencies

```bash
pip install -r requirements.txt
```

### 4 — Configure Environment Variables

Create a `.env` file in the project root:

```env
SECRET_KEY=your-django-secret-key-here
DEBUG=True
```

### 5 — Run Migrations & Start Server

```bash
python manage.py migrate
python manage.py createsuperuser   # optional
python manage.py runserver
```

### 6 — Open in Browser

```
http://127.0.0.1:8000/
```

---

## ☁️ Deployment

### Render (Recommended)

The `Procfile` is already configured:

```
web: gunicorn geopotent.wsgi:application --log-file -
```

1. Push to GitHub
2. Create a new **Web Service** on [Render](https://render.com)
3. Set environment variables: `SECRET_KEY`, `DEBUG=False`
4. Render auto-detects the Procfile and deploys

### Vercel

`vercel.json` is included and routes all traffic through `geopotent/wsgi.py`. Run:

```bash
vercel --prod
```

> ⚠️ SQLite is ephemeral on serverless platforms. For production, switch to **PostgreSQL** (Render Postgres, Supabase, or Neon).

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Django 4.x (Python) |
| **Database** | SQLite (dev) · PostgreSQL (prod-ready) |
| **Auth** | Django built-in + custom role-based profiles |
| **External APIs** | SoilGrids REST API · Open-Meteo Archive API |
| **Energy Modelling** | NumPy, Pandas, custom PV + Wind physics |
| **Visualisation** | Matplotlib (base64 embedded in HTML/PDF) |
| **PDF Export** | xhtml2pdf + Matplotlib |
| **Static Files** | WhiteNoise (production serving) |
| **Frontend** | HTML5, CSS3, JavaScript |
| **Deployment** | Render (Gunicorn) · Vercel (serverless) |
| **Config Management** | django-environ (.env) |

---

## 🔮 Roadmap

- [ ] 🗺️ Interactive map-based land selection (Leaflet.js / Google Maps)
- [ ] 🔋 Battery storage modelling and ROI calculator
- [ ] 📊 Admin analytics dashboard (platform-wide usage insights)
- [ ] 💬 Real-time proposal chat between landowners and builders
- [ ] 🏦 Financial projection module (payback period, NPV, IRR)
- [ ] 🔔 Email / SMS notifications for proposal status changes
- [ ] 📱 Progressive Web App (PWA) for mobile access
- [ ] 🌐 Multi-language support (Tamil, Hindi, etc.)
- [ ] 🐘 PostgreSQL migration guide for production
- [ ] 📤 Excel / CSV export of analysis results

---

## 👨‍💻 Author

<div align="center">

**SHREYAAS**
*GeoPotent — Smart Land Analysis Platform*

<p>
  <a href="https://github.com/your-username"><img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white"/></a>
  <a href="mailto:your-email@example.com"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white"/></a>
  <a href="https://linkedin.com/in/your-profile"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white"/></a>
</p>

</div>

---

<div align="center">

*Built to turn idle land into intelligent opportunity — one coordinate at a time.*

</div>
