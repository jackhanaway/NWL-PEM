# 🧮 2025 Great Plains East Pitcher Evaluation Metric and Scouting Grades

**Author:** Jackson Hanaway  
**Date:** November 2025  

---

## Introduction

This past summer, I worked with the Eau Claire Express of the Northwoods League as an assistant coach and analytics coordinator, where I spent every game of the summer with the team, creating scouting reports of opposing teams daily. Considering the volatile nature of the Northwoods (players coming in and out, getting recruited, draft workouts, etc.), it is sometimes difficult to truly evaluate a players' season performance using a tangible metric like WAR. The purpose of this project was to design a comprehensive player evaluation metric for the Great Plains East Division of the Northwoods League, aimed at capturing a player’s overall value by integrating statistical performance with scouting-informed context.


This project was inspired by learning to calculate advanced baseball metrics such as WAR and DICE (Defense-Independent Component ERA) during my sport analytics coursework at the University of Tennessee. Though it was not possible to directly apply WAR formulas to the data available from the Northwoods League, I sought to create a pitching metric that captures both actual performance and sample size reliability.

---

## Methodology Overview

### Data Collection and Standardization

Data comes from publicly available individual player stat CSVs for the 2025 Great Plains East teams: the Eau Claire Express, Duluth Huskies, La Crosse Loggers, Thunder Bay Border Cats, Rochester Honkers, and Waterloo Bucks. Data was cleaned in Microsoft Excel and analyzed in R Markdown (`GPE_Pitching.Rmd`). Pitchers with fewer than 15 innings pitched were excluded to maintain reasonable sample size while keeping small-innings pitchers for context. Though a benchmark such as 20 innings may have been a better choice for sample size purposes, I wanted to include pitchers from Eau Claire with 15-20 innings so that I could better contextualize the scores. The final metric integrates a pitcher’s underlying performance (strikeouts, walks, and home runs allowed) with a Defense-Independent Component ERA (DICE) adjustment. Each variable was standardized to a z-score, then combined using the following weighted formula:

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
```

Each component of the pitching score was chosen based on its predictive relevance to pitcher effectiveness and stability within the Northwoods League. Weights reflect both the strength of correlation to run prevention and theoretical importance in evaluating pitcher skill.

ERA (−0.15): ERA captures overall run prevention, but since it is heavily team and defense-dependent, it was given a moderate negative weight. It still provides useful context but should not dominate the model.

WHIP (−0.20): WHIP directly measures baserunner suppression (walks + hits per inning). It’s more consistent than ERA and highly indicative of command and contact management, warranting a stronger negative weight.

K/9 (+0.10): Strikeout rate is a key marker of dominance and “stuff.” Since this model could be useful in recruiting pitchers at the college level, I figured K/9 should have a decent weight to quantify how each pitcher's stuff faired against Northwoods competition. A moderate positive weight rewards pitchers who demonstrate the ability to miss bats consistently.

BB (−0.05): Walks indicate command issues but are already indirectly reflected in WHIP and DICE. A small negative weight prevents redundancy while still penalizing poor control.

H (−0.05): Hits allowed offer limited independent insight once WHIP and BAA are included. This variable was lightly weighted to maintain a small penalty for consistently hard contact.

FPS% (+0.05): First-pitch strike percentage measures early count leverage and pitch efficiency. A small positive weight encourages pitchers who get ahead and control plate appearances. This metric was particularly relevant for our team on the coaching side, and since this metric seeks to evaluate performance inside of the Northwoods League, I figured it deserved inclusion.

IP (+0.10): Innings pitched reflects durability and sample size reliability. A moderate positive weight rewards pitchers who sustained performance over longer outings and larger samples.

BAA (−0.10): Batting average against isolates opponent contact quality. A midrange negative weight penalizes pitchers allowing frequent base hits despite decent command metrics.

DICE (−0.40): The most heavily weighted component, DICE (Defense-Independent Component ERA) isolates skill from defensive and random variance. Its strong negative weight ensures the model prioritizes sustainable, defense-independent performance. DICE focuses on outcomes a pitcher can control—strikeouts, walks, hit-by-pitches, and home runs—removing the noise created by team fielding or luck. By emphasizing DICE, the metric rewards pitchers who consistently prevent runs regardless of team context or small sample fluctuations. DICE and its cousin FIP are among my favorite metrics for evaluating pitchers who can consistently "get it done", and control what they can control.

To improve interpretability, I decided to scale the score in a similar manner that stats like WRc+ and ERA+ are weighted in MLB context, so that 100 represents the league average, with each 15-point increment corresponding roughly to one standard deviation above or below average. Since this study only covers data from one of the four Northwoods League divisions, "league average" signifies average production from this division. This makes the metric intuitive and easy to interpret, similar to widely used statistics like OPS+ or ERA+, allowing quick comparison of pitchers’ performance relative to their peers.

**Interactive Plot of Pitching Score**

[GPE-Pitching-Interactive.html](https://jackhanaway.github.io/NWL-PEM/GPE-Pitching-Interactive.html)

**Pitching Score vs. Innings Pitched**

To visualize the relationship between pitcher workload and performance, I plotted the pitching score against total innings pitched. Each point represents an individual pitcher in the Great Plains East Division, allowing comparison of both durability and overall effectiveness.

A linear regression was fitted to the data to examine any potential trend between innings pitched and pitching score. The resulting R² of 0.06 reflects that a pitcher's innings pitched account for about 6-7% of the variation in Great Plains East pitching scores, though innings pitched serves as a good benchmark to contrast perfomance and durability, while visualizing outlier performers. The p-value of 0 confirms the statistical significance of the regression model in the R environment, though in practical terms it reflects the structure of the fitted model rather than a meaningful predictive relationship.

This plot highlights that high or low GPE Pitching Scores are not simply a function of innings pitched; rather, the scores reflect underlying performance metrics and DICE adjustments. Pitchers with fewer innings can still achieve high scores if their underlying metrics are strong, reinforcing the metric’s ability to capture quality of performance independent of sample size.
---

****Scouting Grade Overview****

In addition to the quantitative pitching score (GPE Pitch Score), I wanted to provide quantitative scouting grades for certain outlier performers. These grades provide context that the data alone cannot fully reflect, including pitch repertoire, delivery, command, in-game decision-making, mound presence, and more factors. 

For this phase of the project, I will generate scouting reports for the top five pitchers based on their GPE Pitching Scores to contextualize their outlier scores. I will also be highlighting their strengths, areas for improvement, and overall potential. Additionally, a few honorable mentions will be included to recognize pitchers who excelled in specific aspects despite slightly lower overall scores. These scouting evaluations complement the metric-driven analysis, offering a comprehensive picture of player performance in the Great Plains East Division.

### #1 – Dawson Hargrove, RHP | GPE Pitching Score: 455.2 | Team: Eau Claire Express | Current School: Southern Illinois (via Arkansas State) | Age: 23 | Height/Weight: 6'3/195 lbs 

In a relatively small sample size, Dawson Hargrove established himself as the most reliable pitcher for the Eau Claire this summer, posting a 1.07 ERA over 25.1 innings in 7 appearances, including 3 starts. Hargroved averaged over a strikeout per inning in those 25.1 innings pitched. A theme common to each of the top 5 scorers in the division, Hargrove has multiple unique aspects to his game that helped him cement himself as an outlier performer. 

## Arsenal

Hargrove boasts a complete north to south arsenal with a healthy pitch mix from a high arm slot, including a 4 seam, splitter, slider, and 12-6 curveball. Hargrove's 4 seam fastball sits from 88-90 MPH, topping out at around 92. He excels at commanding the fastball up in the strike zone, and tunneling his offspeeds off of it. Hargrove's 4 seam routinely registers outlier induced vertical break, consistently topping 20 inches of IVB, and released it from a near 7 foot release height on average. This shape complemented perfectly with his offspeeds, the most effective of which being his 80 MPH splitter. Hargrove executed his splitter for consistent strikes, low spin rate (1000-1300) combined with a fading, tumbling shape. Hargrove is also comfortable with a sweeping slider from 81-84 MPH, and a 12-6 curveball with heavy vertical drop. 

## Intangibles

Having had the opportunity to work with Hargrove in Eau Claire, I was able to gauge two key proponents to his success: he knows how to use his arsenal, and he pitches with emotion. Hargrove's pitch arsenal and shapes resemble a Northwoods League equivalent of an MLB north-to-south arsenal, and his eye-popping GPE Pitching Score is a testament to his ability to execute said arsenal. While some negative body language may occasionally seep through from a bad call, Hargrove is on the mound looking to dominate his opponent, and has a tangible mound presence. Hargrove's lethal combination of a strong mental game and a refined north-south arsneal led to him dominating the Great Plains East division with the top GPE Pitching Score. 

## MLB Comparison: Trey Yesavage

Hargrove's arsenal of high-IVB fastballs, complemented by a healthy mix of low or negative IVB offspeed offerings bears striking similarities to Toronto's Trey Yesavage. The two share the same tall and lanky stature, though Hargrove will still need to grow into his body to reach his maximum velocity potential.   


### #2 – Zack Serup, LHP | GPE Pitching Score: 412.1 | Team: Rochester Honkers | School: Western Kentucky (via Ventura JC) | Age: 21 | Height/Weight: 6'3/195 lbs

Zack Serup was undoubtedly the best pitching option for the Rochester Honkers this summer. In his sample size of 27.1 innings, Serup posted a 0.66 ERA and 0.80 WHIP in 5 appearances, all starts. Serup offers a north to south arsenal, leaning heavily on his mid to upper 80s fastball, high-IVB fastball and gyro slider. Serup's outlier quality was his excellent command, issuing only 5 walks, the fewest of any pitcher above 25 IP. 

## Arsenal

Serup uses 4 pitches: 4-seam, slider, changeup, and a slow 12-6 cuveball. His primary offering is his 4-seam fastball ranging from 84-87, topping 88 MPH, with excellent induced vertical break averaging 19-20 inches, occasionally reaching the 24-25 range. Serup's slider has a unique shape, a slow sweeper with varying horizontal movement, and consistent IVB around 0-3 inches. Would occasionally flash slow get-me-over curve around 67-68 MPH, and is still developing feel for the changeup. 

## Intangibles

I faced Serup twice while with the Express, and both times he was able to tear through our lineup leaning heavily on his fastball. Getting feedback from our hitters, they would insist that the fastball shape is flat, though I would try explain the ride was leading to us swinging under the pitch, leading to popouts and strikeouts. Serup's offspeeds served as a way to set up his fastball, as the ride gave him deceptive perceived velocity. As far as his demeanor, Serup looked relaxed and at-ease while on the mound, letting the shape of his fastball play into our swings resulting in quick outs. 


## MLB Comparison: Alex Vesia

Though the two pitchers have contrasting mound presences, the similarities between these two arsenals are palpable. Serup and Vesia both leverage their high IVB fastballs at a heavy usage rate, and find ways to get outs without overpowering reads from the radar gun. These two pitchers also excel at using offspeeds to set up and enhance the shapes of their fastballs. Outlier ride fastballs proved effective in the Northwoods in 2025, but Serup will need to develop fastball velocity and feel for a pitch with armside run away from a righty to be able to pitch at the next level.


### #3 – Cohen Gomez, RHP | GPE Pitching Score: 372.1 | Team: Eau Claire Express | School: Stanford | Age: 20 | Height/Weight: 6'3/212 lbs

Cohen Gomez posted the highest GPE Pitching Score out of any pitcher in the dataset with more than 30 innings pitched. The big right hander was a staple for Eau Claire's rotation this summer, pitching to a 3.70 ERA over 48.2 innings. Gomez had the 4th lowest DICE in the division, which was uncharacteristic of pitchers with his sample size. The graph below contrasts each pitcher's innings pitched on the x-axis, with their Defensive Independent Component ERA on the y-axis. What makes his result especially impressive is the larger workload (48.2 IP) compared to most other top performers, who generally logged between 15 and 25 innings. His consistency over a significantly greater sample size suggests his efficiency was sustainable rather than the product of small-sample variance. 

[🔍 View Interactive DICE Plot](https://jackhanaway.github.io/NWL-PEM/GPE-DICE-Interactive.html)

## Arsenal

Gomez has a unique delivery, coming set in the windup by internally rotating his front hip, and rocking into a load in his back leg before a high leg kick and over-the-top finish. At first glance, it almost looks like a balk, but this shuffle into his delivery messes with hitter's timing and gives Gomez repeatability in his delivery. Gomez primarily uses 5 pitches: 4 seam fastball, 2-seam fastball, slider, split-change, and 12-6 curveball, and as the summer progressed, Gomez learned how to sequence his arsenal. Gomez's fastballs will sit from 87-90 MPH, reaching 92-93 with Eau Claire, and while there is more velocity in the tank to be developed, he is able to sustain his velocity deep into games. His 4 seam generates good ride from a high release point, giving him deceptive perceived velocity. His 2-seam shape is still developing, though it worked to show hitters a different fastball shape depending on hitter handedness, and tendencies against the 4-seam. Gomez's best offspeed is "death ball" slider, at around 80-83 MPH. His slider serves as more of a sharp, up to down gyro ball as opposed to a traditional sweeper, and Gomez was able to play this pitch exceptionally off of his ride fastball. Gomez's split-change was also a formidable offering, as he could execute the changeup off of his fastball to both righties and lefties, as well as kill velocity and spin. In a league featuring a high concentration of developing arms, the ability of a pitcher to locate a changeup to a batter of his same handedness led to good individual results from those pitchers. Gomez would also flash a 12-6 curveball at around 77 MPH, with good induced vertical break. Though it mostly served as a get-me-over this summer, it is Gomez's only pitch consistently above 2000 RPMs. If Gomez is able to leverage his frame better to generate more velocity and spin rate, the curveball has potential to turn into a lethal offering.

## Intangibles

Gomez's mound presence is the most polarizing and essential part to his pitching. His large frame, unique and repeatable windup, and interesting arsenal made him a very tough at bat for Northwoods competition. Gomez starts his outings like a bull in a rodeo, with palpable intensity visible from his body language. When Gomez is pitching, his intensity brings out the best in his defense; his defenders want to make plays for him. Gomez is very vocal on the mound, though it is only ever directed positively towards his own team, and never at the opposition. Though scouts might reason that Gomez may not throw as hard as his frame suggests he should, his pitch execution skills are elite, using his fastball to set up offspeeds, and vice versa. Coming from Stanford, Gomez is a smart pitcher with plenty of room to develop into his frame. If Eau Claire had made the Northwoods League championship game, I would vouch to have Gomez starting that game.

## MLB Comparisons: Lance Lynn, Trevor Megill

Gomez is an interesting prospect, in the sense that he has proven collegiate level pitchability as an underclassman, despite having clear potential to improve his velocity. His execution ability and mound presence draw comparisons to Lance Lynn, an old-fashioned pitcher who's pitchability enhanced his arsenal. I included Brewers closer Trevor Megill as a testament to Gomez's potential. Gomez is a big, strong arm with good work ethic; with proper development it would not suprise me to see Gomez reach the mid to upper 90s by his draft year. He also reflects the intensity of these two arms, in the sense that he serves as a field general on the baseball field. Gomez was easily one of the arms most projectable to professional baseball that I saw in the Northwoods. 










