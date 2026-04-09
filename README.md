Interactive A/B Testing Dashboard
A browser-based tool for analyzing experiment results with live statistical testing — no backend, no install, no dependencies. Open the HTML file and start testing.
![Dashboard Screenshot](screenshots/dashboard.png)
🔗 Live Demo ← replace with your GitHub Pages URL
---
What it does
Upload any A/B test CSV and instantly visualize results — or explore with built-in sample data
Runs a Welch's t-test from scratch (no stats library) and reports p-value, 95% confidence interval, lift %, and estimated statistical power
Live filters by device, country, and variant — every chart and stat recalculates instantly
4 visualizations: daily conversion rate trends, sessions vs conversions, revenue distribution (min/Q1/median/mean/Q3/max), and a per-device segment breakdown
Dark mode supported out of the box via CSS variables
---
Screenshots
Dashboard overview	Filtered by device
![Overview](screenshots/dashboard.png)	![Filtered](screenshots/filtered.png)
---
Tech stack
Layer	Technology
UI	Vanilla HTML5, CSS3 (CSS variables, responsive grid)
Charts	Chart.js 4.4
CSV parsing	PapaParse 5.4
Statistics	Welch's t-test, CI, power — implemented from scratch in JS
Hosting	GitHub Pages (static, zero config)
No npm. No build step. No framework. Just open `index.html`.
---
How to run
Option 1 — Local:
```bash
git clone https://github.com/yourusername/ab-testing-dashboard.git
cd ab-testing-dashboard
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```
Option 2 — Live demo:
Visit the GitHub Pages link above. No setup required.
---
Using your own data
Click Upload CSV and select a file with these columns:
```csv
variant,device,country,converted,revenue,date
control,mobile,US,0,0,2024-01-15
variant,desktop,GB,1,89.50,2024-01-15
```
Column	Values
`variant`	`control` or `variant`
`device`	`mobile`, `desktop`, or `tablet`
`country`	`US`, `GB`, `CA`, `AU` (or any string)
`converted`	`1` = converted, `0` = did not
`revenue`	Dollar amount if converted, `0` otherwise
`date`	`YYYY-MM-DD`
A ready-to-use sample file is included: `sample_data.csv`
---
Statistical methodology
The dashboard implements Welch's t-test — chosen over Student's t-test because it does not assume equal variance between the control and variant groups, which is almost never true in real experiments.
For each filter state it computes:
p-value — probability of observing this difference (or greater) under the null hypothesis
95% confidence interval — the range the true conversion rate difference likely falls within
Lift % — relative improvement of variant over control: `(CVR_B - CVR_A) / CVR_A`
Estimated power — probability the test would detect a real effect of this size
Statistical significance threshold: p < 0.05.
---
Project structure
```
ab-testing-dashboard/
├── index.html          # entire app — one self-contained file
├── sample_data.csv     # 200-row sample dataset
├── README.md
└── screenshots/
    ├── dashboard.png
    └── filtered.png
```
---
What I'd add next
Date range picker — filter results to a specific experiment window
Chi-squared test — better suited for pure conversion rate comparisons on large samples
Bayesian A/B testing mode — show probability that variant beats control instead of a binary p-value
Sample size calculator — tell you how many more sessions are needed to reach significance
Export to PDF — one-click report generation for stakeholders
---
Why this project
A/B testing is one of the most common analytical workflows in product and growth teams, but most engineers rely on third-party tools (Optimizely, statsig, etc.) without understanding what's happening under the hood. Building this from scratch — including the t-test math — made that concrete for me.
---
License
MIT — use it, fork it, ship it.
