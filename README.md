# Council Waste Operations Dashboard
**Project 5 — Looker Studio | Real-world municipal data cleaning + dashboarding**

A live dashboard analyzing waste collection data from a UK local authority (Leeds City Council), covering April 2008 to March 2009. Built to practice cleaning genuinely messy real-world data and turning it into a decision-ready operations dashboard.

*(https://datastudio.google.com/s/hanhTOMHwgE)#)** *(add your share link here)*

---

## The business question

Local councils manage waste collection across hundreds of sites, schools, libraries, care homes, and offices, each generating both general waste and recyclable card. Without a central view, it's hard to answer basic questions:

- Which departments generate the most waste?
- Is recycling (card) actually being separated out, or mostly going to general waste?
- Are bin sizes matched to actual usage, or are some bins over/undersized?
- Which individual sites need the most attention?

This project turns twelve months of raw collection records into a dashboard that answers all four.

## About the data

The raw file (`data/raw_waste_data.csv`) is a real, publicly released council dataset: 641 rows covering 367 individual sites across 12 council directorates (Learning & Leisure, Social Care, City Services, Schools, and others), logged monthly from April 2008 to March 2009, split by bin size and waste type (General Waste vs. Card/Recycling).

Being real operational data, it came with the kind of problems you actually run into on the job, not the clean, pre-packaged kind you get from a tutorial dataset.

### Data cleaning steps
- Removed 2 fully blank trailing rows with no data at all
- Standardized inconsistent bin type labels (`1100L` and `1100LW` were both typos for `1100L-W`)
- Trimmed stray whitespace from text fields (directorate, site name, bin type)
- Reshaped the data from wide format (12 separate month columns) into **tidy long format** — one row per site/bin/waste type/month — since that's what proper dashboarding tools need for time-series charts
- Removed 792 rows representing genuinely missing months (no reading taken), while keeping true zero-tonnage months, since "no data collected" and "bin not used that month" are different facts
- Verified no negative values; checked outliers (up to ~16.8 tonnes) against site size and kept them, they reflect real large-site collections, not data errors

Cleaned files:
- `data/waste_cleaned_long.csv` — tidy format, used to build the dashboard
- `data/waste_cleaned_wide.csv` — same fixes, original wide layout kept for reference

## What's in the dashboard

- **Scorecards** — total tonnage, sites tracked, General Waste total, Card/Recycling total
- **Monthly trend** — General Waste vs. Card tonnage, April 2008 to March 2009
- **Tonnage by directorate** — which council departments generate the most waste
- **Tonnage by bin type** — how much each bin size actually contributes
- **Share of waste by bin type** — a proportion view of the same breakdown
- **Top sites table** — individual sites ranked by total tonnage collected

## Key findings

- Total waste collected across the year: **2,027.6 tonnes**
- General Waste made up **~82%** of total tonnage (1,661.4t) versus **~18%** for Card/Recycling (366.2t), suggesting real room to grow recycling participation
- The large **1100L-W** bins account for the vast majority of tonnage collected, roughly 74% of the total, meaning bin-size strategy should focus there first
- **Learning & Leisure** and **Social Care** are the two highest-waste directorates, together generating close to half of all council waste in the dataset

## Tools used
- **Excel / Python (pandas)** — initial data inspection and cleaning
- **Google Sheets** — hosting the cleaned data source
- **Looker Studio** — live, connected dashboard
- <img width="512" height="384" alt="WOP Dashboard" src="https://github.com/user-attachments/assets/96f1222f-71ab-4b90-80b2-9663d127425e" />
