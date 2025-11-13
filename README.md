# 🧮 2025 Great Plains East Pitcher Evaluation Metric and Scouting Grades

**Author:** Jackson Hanaway  
**Date:** November 2025  

---

## Introduction

This past summer, I worked with the Eau Claire Express of the Northwoods League as an assistant coach and analytics coordinator, attending every game and creating daily scouting reports of opposing teams. Considering the volatile nature of the Northwoods League (players coming in and out, drafts, workouts, etc.), it is sometimes difficult to evaluate a player’s season performance using traditional metrics like WAR. The purpose of this project was to design a comprehensive player evaluation metric for the Great Plains East Division, integrating statistical performance with scouting-informed context.

This project was inspired by my sport analytics coursework at the University of Tennessee, where I learned to calculate advanced metrics such as WAR and DICE (Defense-Independent Component ERA). Though WAR formulas could not be directly applied to Northwoods League data, I created a pitching metric that captures both actual performance and sample size reliability.

---

## Methodology Overview

### Data Collection and Standardization

Data comes from publicly available individual player stat CSVs for the 2025 Great Plains East teams: Eau Claire Express, Duluth Huskies, La Crosse Loggers, Thunder Bay Border Cats, Rochester Honkers, and Waterloo Bucks. Data was cleaned in Microsoft Excel and analyzed in R Markdown (`GPE_Pitching.Rmd`). Pitchers with fewer than 15 innings pitched were excluded to maintain reasonable sample size while keeping small-innings pitchers for context. The final metric integrates a pitcher’s underlying performance (strikeouts, walks, and home runs allowed) with a Defense-Independent Component ERA (DICE) adjustment. Each variable was standardized to a z-score, then combined using the following weighted formula:

```r
weights_pitching_v2 <- c(
  ERA = -0.15,
  WHIP = -0.20,
  K.9 = 0.10,
  BB = -0.05,
  H = -0.05,
  FPS. = 0.05,
  IP = 0.10,
  BAA = -0.10,
  DICE = -0.40
)
