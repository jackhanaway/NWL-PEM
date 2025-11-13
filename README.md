# 🧮 2025 Great Plains East Pitcher Evaluation Metric and Scouting Grades

**Author:** Jackson Hanaway  
**Date:** November 2025  

---

****Introduction****

This past summer, I worked with the Eau Claire Express of the Northwoods League as an assistant coach and analytics coordinator, where I spent every game of the summer with the team, creating scouting reports of opposing team daily. Considering the volatile nature of the Northwoods (players coming in and out, getting recruited, draft workouts, etc.), it is sometimes difficult to truly evaluate a players' season performance using a tangible metric like WAR. The purpose of this project was to design a **comprehensive player evaluation metric** for the **Great Plains East Division of the Northwoods League**, aimed at capturing a player’s overall value by integrating **statistical performance** with **scouting-informed context**. 


This project was inspired by learning to calculate advanced baseball metrics such as **WAR** and **DICE (Defense-Independent Component ERA)** during my sport analytics coursework at the University of Tennessee. Though it was not possible to directly apply WAR formulas to the data available from the **Northwoods League**, I sought to create a pitching metric that captures both **actual performance** and **sample size reliability**.  

---

****Methodology Overview****

**Collection and Standardization**

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

Each component of the pitching score was chosen based on its predictive relevance to pitcher effectiveness and stability within the Northwoods League. Weights reflect both the strength of correlation to run prevention and theoretical importance in evaluating pitcher skill. 

ERA (−0.15)
ERA captures overall run prevention, but since it is heavily team and defense-dependent, it was given a moderate negative weight. It still provides useful context but should not dominate the model.

WHIP (−0.20)
WHIP directly measures baserunner suppression (walks + hits per inning). It’s more consistent than ERA and highly indicative of command and contact management, warranting a stronger negative weight.

K/9 (+0.10)
Strikeout rate is a key marker of dominance and “stuff.” Since this model could be useful in recruiting pitchers at the college level, I figured K/9 should have a decent weight to quantify how each pitcher's stuff faired against Northwoods competition. A moderate positive weight rewards pitchers who demonstrate the ability to miss bats consistently.

BB (−0.05)
Walks indicate command issues but are already indirectly reflected in WHIP and DICE. A small negative weight prevents redundancy while still penalizing poor control.

H (−0.05)
Hits allowed offer limited independent insight once WHIP and BAA are included. This variable was lightly weighted to maintain a small penalty for consistently hard contact.

FPS% (+0.05)
First-pitch strike percentage measures early count leverage and pitch efficiency. A small positive weight encourages pitchers who get ahead and control plate appearances. This metric was particularly relevant for our team on the coaching side, and since this metric seeks to evaluate performance inside of the Northwoods League, I figured it deserved inclusion.

IP (+0.10)
Innings pitched reflects durability and sample size reliability. A moderate positive weight rewards pitchers who sustained performance over longer outings and larger samples.

BAA (−0.10)
Batting average against isolates opponent contact quality. A midrange negative weight penalizes pitchers allowing frequent base hits despite decent command metrics.

DICE (−0.40)
The most heavily weighted component, DICE (Defense-Independent Component ERA) isolates skill from defensive and random variance. Its strong negative weight ensures the model prioritizes sustainable, defense-independent performance. DICE focuses on outcomes a pitcher can control—strikeouts, walks, hit-by-pitches, and home runs—removing the noise created by team fielding or luck. By emphasizing DICE, the metric [Uploading GPE-Pitching.html…]()
rewards pitchers who consistently prevent runs regardless of team context or small sample fluctuations. DICE and its cousin FIP are among my favorite metrics for evaluating pitchers who can consistently "get it done".

To improve interpretability, I decided to scale the score in a similar manner that stats like WRc+ and ERA+ are weighted in MLB context, so that 100 represents the league average, with each 15-point increment corresponding roughly to one standard deviation above or below average. Since this study only covers data from one of the four Northwoods League divisions, "league average" signifies average production from this division. his makes the metric intuitive and easy to interpret, similar to widely used statistics like OPS+ or ERA+, allowing quick comparison of pitchers’ performance relative to their peers.

---
****Interactive Plot of Pitching Score****

https://jackhanaway.github.io/NWL-PEM/GPE-Pitching-Interactive.html

