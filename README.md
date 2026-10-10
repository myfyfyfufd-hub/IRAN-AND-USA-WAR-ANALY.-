# Iran–US Conflict News Analysis

Cleaning, analysis and an Excel dashboard for a dataset of 2,286 news items about the Iran–US/Israel conflict (collected via Bing, RSS and a BBC scrape; dated articles span May 2025 to June 2026).

## What's inside

| File | Purpose |
|---|---|
| `iran_us_news_dashboard.xlsx` | Excel dashboard, summary report, analysis tables, clean and original data |
| `iran_us_news_analysis.py` | Pandas script: load, clean, explore, export |
| `iran_us_news_analysis.sql` | PostgreSQL: staging table, cleaning views, data-quality checks, analysis |

## Key findings

- 2,194 unique articles from 203 outlets after flagging repeated titles.
- BBC supplies about half of the articles; the top 5 outlets supply 67%.
- Most common themes (keyword rules): military strikes, Israel/Lebanon, Hormuz/oil, ceasefire talks.
- Only 33% of articles have a publish date, so time trends cover that subset only.

## Cleaning approach

- No rows deleted; repeated titles and texts are flagged.
- Missing dates are not imputed.
- Only clearly identical outlet names are merged (e.g. `BBC World` → `BBC`).
- Themes are rule-based keyword flags, not a topic model.

## How to run

**Python**
```bash
pip install pandas
python iran_us_news_analysis.py iran_us_news_dataset.csv
```
Outputs are written to `analysis_output/`.

**SQL (PostgreSQL 13+)**
1. Load the CSV into `stg_iran_us_news` (see the header of the `.sql` file).
2. Run the file top to bottom.

## Notes

- The raw CSV is not included because it contains full text of copyrighted news articles. Add your own copy next to the script to run it.
- Original data cells longer than 32,767 characters are truncated in the Excel file because of Excel's limit.
