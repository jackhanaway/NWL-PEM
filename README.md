# 🧮 2025 Great Plains East Pitcher Evaluation Metric and Scouting Grades

**Author:** Jackson Hanaway  
**Date:** November 2025  

---

Introduction

This past summer, I worked with the Eau Claire Express of the Northwoods League as an assistant coach and analytics coordinator, where I spent every game of the summer with the team, creating scouting reports of opposing team daily. Considering the volatile nature of the Northwoods (players coming in and out, getting recruited, draft workouts, etc.), it is sometimes difficult to truly evaluate a players' season performance using a tangible metric like WAR. The purpose of this project was to design a **comprehensive player evaluation metric** for the **Great Plains East Division of the Northwoods League**, aimed at capturing a player’s overall value by integrating **statistical performance** with **scouting-informed context**. 


This project was inspired by learning to calculate advanced baseball metrics such as **WAR** and **DICE (Defense-Independent Component ERA)** during my sport analytics coursework at the University of Tennessee. Though it was not possible to directly apply WAR formulas to the data available from the **Northwoods League**, I sought to create a pitching metric that captures both **actual performance** and **sample size reliability**.  

---

Methodology Overview

My data comes from the publicly available individual player stat .csvs from each of the 2025 Great Plains East teams: the Eau Claire Express, Duluth Huskies, La Crosse Loggers, Thunder Bay Border Cats, Rochester Honkers, and Waterloo Bucks. The data was cleaned inside of Microsoft Excel, and all analysis was performed in **R Markdown** using [`GPE_Pitching.Rmd`](./GPE_Pitching.Rmd). I decided to filter my data by excluding all pitchers with less than **15 innings pitched**. Though a benchmark such as 20 innings may have been a better choice for sample size purposes, I wanted to include pitchers from Eau Claire with 15-20 innings so that I could better contextualize the scores. 

Though I went through several versions before arriving at my finished formula, the final metric integrates a pitcher’s underlying performance (strikeouts, walks, and home runs allowed) with a **Defense-Independent Component ERA (DICE)** adjustment. Each variable was standardized to a z-score to allow fair comparison across categories and then combined using the following weighted formula:

weights_pitching_v2 <- c(
  ERA  = -0.15,
  WHIP = -0.20,
  K.9  =  0.10,
  BB   = -0.05,
  H    = -0.05,
  FPS. =  0.05,
  IP   =  0.10,
  BAA  = -0.10,
  DICE = -0.40  # heavily weighted (lower DICE is better)
)

