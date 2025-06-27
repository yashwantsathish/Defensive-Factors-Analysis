# Defensive Efficiency: A Multi-Season Analysis of Key Predictors

This project investigates the statistical drivers of team defensive efficiency in the NBA from 2020–21 through 2024–25. Using advanced and opponent metrics from the NBA Stats API, the analysis identifies which defensive factors most strongly influence a team's **Defensive Rating** (points allowed per 100 possessions).

---

## 🎯 Purpose

Prompted by a coach's question — *"Is defensive rebounding truly a key to great defense?"* — this study aims to answer that and more using league-wide data. By evaluating metrics over a five-season span, we provide robust insights that avoid year-to-year noise and offer clear direction for building or evaluating a defensive system.

---

## 📊 Key Findings

- **Opponent Effective Field Goal % (eFG%)** has the strongest impact on Defensive Rating: teams that limit opponent shot quality perform better defensively.
- **Opponent Turnover Rate** also significantly improves Defensive Rating by limiting shot attempts.
- **Defensive Rebounding %** helps, but its impact is smaller in comparison to shot quality and turnovers.
- **Opponent Free Throw Rate** worsens Defensive Rating, suggesting disciplined defense matters.

All variables were standardized for interpretability. The regression controls for season-to-season shifts in league trends.

---

## 📦 Features

- Data collected via [`hoopR`](https://github.com/sportsdataverse/hoopR) from NBA.com.
- Custom opponent metrics calculated from box score-level team stats.
- Multiple linear regression with standardization and seasonal controls.
- Visualizations tailored for coaches and non-technical stakeholders.

---

## 📁 Structure

- `DefensiveRatingStudy.qmd` or `.Rmd`: Main script with all code blocks and commentary.
- `figures/`: Contains presentation-ready plots.
- `data/`: Raw and processed versions of season-by-season team metrics.
- `report.html`: Rendered final output for easy web review.

---

## 🛠️ How It Works

```r
# Load & join advanced + opponent data
nba_leaguedashteamstats(...)

# Compute key opponent stats:
# Opponent eFG% = (FGM + 0.5 * 3PM) / FGA
# Opponent TOV% = TOV / (FGA + 0.44 * FTA + TOV)
# Opponent FT Rate = FTA / FGA

# Run regression with season dummies:
lm(DefRtg ~ scale(DRB) + scale(Opp_eFG) + scale(Opp_TOV) + scale(Opp_FTRate) + Season, data = full_data)
