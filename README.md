# Hamburg Overhead Door — Operations Dashboard

Real-time operations intelligence for Hamburg Overhead Door and partner companies.

## Features

- **Multi-Company Dashboard** — Hamburg, Wayne-Dalton of Syracuse, Buffalo Garage Door Solutions
- **Real-Time Monitoring** — Staff attendance, service capacity, install schedule, fleet efficiency
- **Operations Metrics** — 30-day trends, year-over-year comparison, revenue analysis
- **Lead Tracking** — Estimator pipeline, Google LSA distribution, service routing

## Dashboard Sections

### Top Level
- **Attendance** — Who's out today, partial absences
- **Ariana's Context** — Real-time service tech capacity
- **LSA Leads** — Google Local Services Ads inbound

### Operations
- **Install Schedule** — 7-day calendar, tech assignments
- **Service Dispatch** — Service calls, tech workload, zone coverage
- **Bid Pipeline** — Quote funnel by stage

### Intelligence
- **Trends** — Service tickets, sales calls, big jobs, revenue (30d + YoY)
- **Fleet Efficiency** — MPG, idle time, fuel costs, vehicle rankings
- **Company Tabs** — Switch between Hamburg, Wayne-Dalton, Buffalo GDS

## Deployment

This dashboard is auto-deployed to Netlify from the main branch.

**Public URL:** [Live Dashboard](https://hod-dashboard.netlify.app) _(update with actual Netlify domain)_

### Local Development

```bash
# Serve locally
python3 -m http.server 8000

# View at http://localhost:8000
```

### CI/CD

- Push to `main` branch triggers automatic Netlify deployment
- GitHub Actions handles the pipeline
- Pull requests get preview deployments

**Required GitHub Secrets:**
- `NETLIFY_AUTH_TOKEN` — Netlify API token
- `NETLIFY_SITE_ID` — Netlify site ID

## Data Freshness

Dashboard refreshes **3x daily**:
- **9:00 AM EST** — Morning refresh
- **1:00 PM EST** — Afternoon refresh
- **5:00 PM EST** — Evening refresh

Overnight (5 PM - 9 AM): No updates.

## Technology

- **Frontend:** HTML5, CSS3, JavaScript (vanilla, no frameworks)
- **Backend:** Python (dashboard generator)
- **Database:** MS SQL Server (192.168.1.15)
- **Deployment:** Netlify

## Security Note

This dashboard is **internal only**. While publicly hosted, it contains operational data for Hamburg Overhead Door and partner companies.

---

Maintained by Cipher (William's automation system)
