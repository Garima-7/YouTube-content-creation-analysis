# 📺 YouTube Content Creation Analysis

A data analytics project that collects real data from YouTube (using YouTube's official API), cleans it, and turns it into an interactive Power BI dashboard — helping content creators figure out what actually works on YouTube.

---

## 🎯 What This Project Does

Every YouTube creator wants to know things like: *Should I make gaming videos or cooking videos? Does video length matter? What time should I post?*

This project answers those questions using **real data** — not guesses. I pulled data on **453 YouTube channels** and **~31,000 videos** across **9 content categories**, cleaned it, and built a dashboard that shows which content strategies actually get results.

The key idea: I focused on **engagement rate** (likes + comments per view) instead of just raw view counts — because a video with 1M views and no engagement isn't necessarily "winning."

---

## ❓ Questions This Project Answers

- Which content categories get the most engagement, and which are oversaturated (lots of videos, low reward)?
- Which channels are top performers, and what do they do differently?
- Does video length affect engagement?
- Do things like description length or number of tags matter?
- Does posting day/time affect performance?
- How has YouTube (channels, uploads, subscribers) grown over time?
- Within one channel, what makes some videos hit and others flop?

---

## 🧰 Tools & Skills Used

| Tool | Used For |
|---|---|
| **Python** (requests, pandas, isodate) | Pulling data from YouTube's API and cleaning it |
| **YouTube Data API v3** | Source of all the data |
| **Power BI** (Power Query + DAX) | Building the dashboard and calculations |
| **Git/GitHub** | Version control and showcasing the project |

**Skills demonstrated:** API integration, data pipeline design, data cleaning & validation, DAX/data modeling, dashboard design, and turning raw data into business insights.

---

## 📊 KPIs & Metrics Used in the Dashboard

**Headline numbers (shown as cards on the dashboard):**
- **Total Channels** — 453
- **Total Videos** — 30.96K
- **Total Categories** — 9
- **Total Views** — 1.84 Trillion
- **Median Subscribers** — 121K
- **Average Engagement Rate** — 2.56%

**Core KPI:**
| KPI | What It Measures |
|---|---|
| **Engagement Rate** | (Likes + Comments) ÷ Views — the main success metric on this dashboard. Measures how much people actually interact with a video, not just watch it |

Engagement Rate is the one true KPI this project is built around — every other metric below exists to explain *why* engagement rate goes up or down.

**Supporting DAX Measures** (calculations that feed the analysis):
| Measure | What It Calculates |
|---|---|
| `average engagement` | Average engagement rate across a set of videos |
| `median description length` | Typical description length, compared across top vs. weak videos |
| `median duration minutes` | Typical video length, used to test if longer/shorter videos perform better |
| `median tag length` | Typical number of tags used per video |

**Calculated Columns** (used to segment and slice the data, not KPIs themselves):
| Column | Purpose |
|---|---|
| `channel_age` | Years since a channel was created |
| `videos per year` | Upload frequency per channel |
| `duration minutes` | Per-video length, in minutes |
| `engagement` | Per-video (likes + comments) ÷ views |
| `publish day of week` | Day the video went live, for timing analysis |
| `Video_rank_within_channel` | Buckets each video as "Popular / Medium / Not Popular" based on its view rank inside its own channel |
| `Video_rank_within_category` | Same idea, but ranked against every other video in its category |

The dashboard's headline KPI cards (Total Channels, Total Videos, Total Categories, Total Views, Median Subscribers, Average Engagement Rate) are simple aggregations shown at the top of each page — the measures and columns above are what let you break those numbers down and explain them.

---

## 🔄 How the Data Was Collected

YouTube doesn't have one single API endpoint that gives you "all videos from all channels." So the data had to be built step by step:

1. **Search** YouTube by keyword (technology, gaming, music, news, etc.) → get channel IDs
2. **Channels API** → get channel details (subscribers, views, country, creation date)
3. **Channels API again** → get each channel's "Uploads" playlist
4. **Playlist Items API** → get every video ID from that playlist
5. **Videos API** → get full details for every video (views, likes, comments, tags, duration)
6. **Video Categories API** → match category IDs to real category names (like "Gaming" or "Comedy")

All of this was automated in Python, with pagination handled so no data was missed even for channels with thousands of videos.

---

## 🧹 Data Cleaning

I checked every column for problems, but only "fixed" things that were actual errors — not things that were just naturally missing (like an optional description a creator chose not to write).

Examples:
- Converted video duration from YouTube's weird format (`PT4M23S`) into normal minutes/seconds
- Removed columns that were useless (like "dislike count," which YouTube no longer shares publicly)
- Left blank descriptions/tags/likes alone — they're optional fields, not data errors, so I excluded them from averages instead of guessing values
- Double-checked things like "did any subscription happen before the channel existed?" (Answer: no — data passed the check)

---

## 💡 Key Insights Found

- **How-to & Style** gets the most total views, but not the best engagement — big reach, but people don't interact as much per view.
- **Gaming** has the best engagement rate despite not having the most videos — an underrated category for creators.
- **News & Politics** has tons of videos but low engagement — more supply doesn't mean more interest.
- Top-performing videos within a channel tend to have **longer descriptions and more tags** than low performers.
- Engagement is highest for videos **under ~45 minutes** and videos posted **between 11 AM–3 PM**.
- **India** has the largest share of channels in this dataset (~60%).
---

## 📁 Project Structure

```
youtube-content-analysis/
│
├── README.md
├── data_creation_python_scripts/     → Python notebooks that pull data from the API
├── data/                             → Collected CSV files (channels, videos, subscriptions, etc.)
├── dashboard/                        → Power BI dashboard file (.pbix)
├── docs/                             → Documentation
└── images/                           → Dashboard images
```

---

## ⚙️ How to Run This Project

1. Get a free API key from [Google Cloud Console](https://console.cloud.google.com/) (enable "YouTube Data API v3")
2. Install requirements:
   ```bash
   pip install pandas requests isodate
   ```
3. Add your API key into the notebooks in `data_creation_python_scripts/`
4. Run the notebooks in order: channels → uploads → videos → categories → subscriptions
5. Open the `.pbix` file in Power BI Desktop to explore the dashboard

---

## 👤 About Me

Built by **Garima Gupta** as a personal data analytics portfolio project — from raw API data to a full business-ready dashboard.
