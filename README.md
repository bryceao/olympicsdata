# Olympics Project

Exploratory data analysis of 120 years of Olympic athlete data (Athens 1896 to Rio 2016) for our EDA with Python class term project.

**Team:** Ezekiel Galvez, Bryce Osborne, Christopher Munoz, Jinbang Bae

## Dataset

`data/olympics.csv`: 271,116 athlete-event records, 135,571 unique athletes, 66 sports, 230 NOCs, Summer and Winter games.
Each row is one athlete in one event at one games.

| Group | Columns |
|---|---|
| Demographics | `sex`, `age`, `height`, `weight` |
| Competition | `games`, `year`, `season`, `city` |
| Classification | `sport`, `event`, `team`, `noc` |
| Outcome | `medal` (Gold / Silver / Bronze, `NA` = no medal) |

## Research questions

1. Do physical attributes (height, weight, age) differ by sport, and do they relate to medaling?
2. How has female participation changed over time, and has the gap closed?
3. What explains differences in national medal performance?
4. Is there a measurable host-country advantage?

The full proposal is in [`olympics_report.pdf`](olympics_report.pdf).

## Repository layout

```
.
├── data/olympics.csv                 raw dataset
├── notebooks/01_olympics_eda.ipynb   import, assess, clean, EDA (source of the report)
├── reports/01_olympics_eda.html      rendered HTML report (the deliverable)
├── olympics_report.pdf               dataset selection report
└── requirements.txt
```

## Cleaning decisions

- Dropped 1,385 exact duplicate rows.
- `medal` of `NA` means no medal, not missing data: recoded to `No medal` plus a binary `won_medal`.
- Height and weight are ~22-23% missing, mostly before 1960, so physical analyses use the 1960+ subset.
- Art Competitions are excluded from physical analyses.
- Team medals are counted once per country (deduplicated by games, event, NOC and medal) for national tallies.

## Run it

```bash
python -m venv .venv
.venv\Scripts\activate          # macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
jupyter lab notebooks/01_olympics_eda.ipynb
```

Export the HTML report:

```bash
jupyter nbconvert --to html notebooks/01_olympics_eda.ipynb --output-dir reports
```

## Status

- [x] Import, assessment, cleaning
- [x] First EDA pass on all four questions (13 figures)
- [ ] Logistic regression of medal status on physical attributes, by sport
- [ ] Host-advantage analysis controlling for delegation size
- [ ] Explicit handling of historical NOCs (URS, GDR, FRG)
- [ ] Interactive plotly figures and final presentation
