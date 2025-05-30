## Project Overview

This project explores how national team success in the FIFA World Cup can be systematically measured and compared using historical performance data from 1930 to 2022. It aims to measure success using stage progression and compare long-term performance across confederations.

A stage-based scoring system is used to quantify how far teams advance in each tournament. Additionally, secondary indicators such as win rate and goal difference per game provide supporting context.

The analysis includes a specific comparison between UEFA and CONMEBOL, two of the most successful football confederations. Through exploratory data analysis and hypothesis testing, the project investigates whether one has historically outperformed the other in terms of World Cup success.

## **Research Question**

**Can a stage-based scoring system systematically measure and compare national team success in the FIFA World Cup across different confederations?**
- Are UEFA teams statistically more successful than CONMEBOL teams in the World Cup?  
- Does FIFA Ranking correlate with tournament performance?


## Motivation  
Football has always been a personal passion, and the FIFA World Cup stands out as the most prestigious and exciting tournament in the sport. This project offers an opportunity to combine that enthusiasm with an academic interest in data science. By analyzing historical World Cup data, the goal is to gain deeper insights into how national team success can be quantified and compared over time. This work also reflects a broader interest in football analytics—a growing field where statistical reasoning and data-driven methods are increasingly shaping how the game is understood and strategized. The project serves as a practical step toward building a career at the intersection of football and data science, offering valuable experience in working with real-world sports data and applying exploratory analysis and hypothesis testing in a structured and meaningful way.


## Methodology

### Installation & Reproducibility

To run this project locally:

1. Clone the GitHub repository  
2. Install the required Python libraries by running:

```
pip install -r requirements.txt
```

3. Execute the notebooks in the following order:
   - `data_process.ipynb` (for preprocessing)
   - `data_visualization.ipynb` (for charts and figures)
   - `hypothesis_testing.ipynb` (for statistical testing)
   - `ml_analysis.ipynb` (for machine learning)


### Data Collection & Preprocessing

The datasets were collected from multiple public sources and harmonized to create a clean master dataset.

**Data Sources:**
- Historical FIFA World Cup results (1930–2022)
- FIFA Rankings (1994–2024)
- Confederation membership data


**Preprocessing Steps:**
- Standardized country names using mapping dictionaries
- Assigned a stage score from 1 to 6 to reflect how far a team advanced in each World Cup, based on the following stage-based scoring system:

  | Tournament Stage     | Score |
  |-----------------------|-------|
  | Group Stage Exit      | 1     |
  | Round of 16           | 2     |
  | Quarter-Finals        | 3     |
  | Semi-Finals           | 4     |
  | Runner-up (Finalist)  | 5     |
  | Champion (Winner)     | 6     |

  This scoring system ensures a consistent and objective measurement of team performance across tournaments and allows systematic comparisons between teams and confederations.
- Created key variables per team:
  - `sum_stage_score_full`: Total stage score across all tournaments
  - `win_rate`: Win ratio across all matches
  - `gd_per_game`: Goal difference per game
- Calculated `avg_rank` for each team using FIFA Rankings (only from 1994 onward)
- Filtered out teams with fewer than 2 tournament appearances

---

## Statistical Analysis

The third stage of the project focuses on examining long-term patterns in World Cup performance using statistical methods. The goal is to evaluate whether measurable indicators of success—such as **stage progression**, **win rate**, and **goal difference per game**—reveal systematic advantages between confederations, particularly between **UEFA** and **CONMEBOL**. In addition, statistical tests are used to explore the relationship between team success and **FIFA rankings**.

---

## How the Data Will Be Used

Each dataset contributes to answering a specific research question by being transformed into indicators of performance. The following is a breakdown of how the data is used:

### 1. Historical World Cup Data (1930–2022)

- **Purpose**: Build the primary measure of success (stage score), and compute win rate and goal difference per game.  
- **Usage**:
  - Assign scores from 1 (Group Stage) to 6 (Champion) for each team’s performance per tournament.
  - Aggregate results by team and confederation.
  - Use match outcomes to calculate win rate and goal difference per game.

### 2. FIFA Rankings (1994–2022)

- **Purpose**: Evaluate how pre-tournament expectations (rankings) align with actual success.  
- **Usage**:
  - Compute each team’s average FIFA ranking across the years they participated post-1994.
  - Correlate these values with post-1994 stage scores using Spearman correlation.

### 3. Confederation Info

- **Purpose**: Compare performance between different global football regions.  
- **Usage**:
  - Group and analyze results by confederation.
  - Visualize and test performance trends (e.g., UEFA vs. CONMEBOL).

These steps enable the use of data not just descriptively, but also to conduct rigorous, testable comparisons that support meaningful insights into long-term patterns of team success at the FIFA World Cup.


## Exploratory Data Analysis (EDA)

To understand the data before testing hypotheses, some basic exploratory analysis was conducted. This included checking for missing values, identifying outliers, and examining the distribution of stage scores.

---

### 1. Missing Value Analysis

![Figure 1: Heatmap of Missing Values](output/Missing%20Value%20Analysis.png)

A heatmap was used to detect missing values in the dataset.  
While the majority of the data is complete, a few columns — including FIFA rankings and post-1994 stage scores — contain missing entries. These are mostly due to data being unavailable for certain teams or tournaments.  
Rows with missing values were handled appropriately depending on the analysis.

---

### 2. Outlier Detection

![Figure 2: Outlier Detection for Total Stage Score](output/Outlier%20Detection.png)

A boxplot was generated to visually inspect potential outliers in total stage scores.  
A few exceptionally high-performing teams stand out as statistical outliers, especially from UEFA. These include teams like Germany and Brazil.  
These values were kept in the dataset, as they represent meaningful historical achievements.

---

### 3. Skewness of the Distribution

The skewness of the total stage score distribution was calculated to assess its symmetry.  
A strong right-skew was observed (**skewness ≈ 1.99**), meaning that most teams have relatively low scores, while a small number have achieved very high totals.  
This reflects the dominance of a few elite teams in World Cup history.

---

### 4. Summary

The dataset is mostly complete and includes some meaningful outliers.  
The distribution of total stage scores is right-skewed, with a few teams consistently performing at a much higher level than the rest.  
These findings helped shape the next steps in visualization and hypothesis testing.


## Data Visualization

### ![Stage Score Distribution by Confederation](output/Stage%20Score%20Distribution%20by%20Confederation.png)  

**Figure 1: Stage Score Distribution by Confederation**

This box plot displays the distribution of stage scores (1 = Group Stage, ..., 6 = Champion) by confederation.

- **CONMEBOL** shows the highest median (~2.5) and the widest spread, indicating frequent deep tournament runs and multiple championships.
- **UEFA** follows with a median around 3 and several high stage scores as outliers, reflecting consistent semifinal and final appearances.
- **CAF**, **AFC**, **CONCACAF**, and **OFC** mostly cluster near the bottom, with medians at 1, signaling regular group-stage exits and only a few outlier performances in later stages.

### ![Average Win Rate by Confederation](output/Average%20Win%20Rate%20by%20Confederation.png)  
**Figure 2: Average Win Rate by Confederation**

This bar chart shows the average match win rates for each confederation across all World Cup tournaments.

- **CONMEBOL** leads with a win rate of **0.43**, reflecting dominant performances across decades.
- **UEFA** follows with **0.37**, also indicating a strong historical record.
- **CAF**, **CONCACAF**, and **AFC** show lower win rates (0.20, 0.18, and 0.15 respectively), highlighting the challenge these regions face against top-tier opponents.
- **OFC** records **0.00**, showing no World Cup match victories, which aligns with its historically limited representation.
- Overall, this distribution aligns with the stage progression seen in Figure 1: confederations that win more often also tend to advance further.


### ![Stacked Histogram of GD per Game by Confederation](output/Stacked%20histogram-%20GD%20per%20Game%20by%20Confederation.png)  
**Figure 3: Stacked Histogram of GD per Game by Confederation**

This histogram shows the distribution of **goal difference per game** (GD/game) for each confederation, grouped in bins of 0.25.

- **CONMEBOL** and **UEFA** dominate the positive side, with most matches resulting in GD values between **+0.5 and +1.5**, suggesting consistent and decisive wins.
- **CAF**, **CONCACAF**, and **AFC** concentrate around **–0.5 to +0.5**, reflecting close games with narrow margins, often indicating parity or struggle against stronger opponents.
- **OFC** appears rarely, confirming the confederation’s minimal World Cup involvement.
- These results support earlier findings: South American and European teams not only win more often (Figure 2), but also win **by larger margins**.


### ![Total Stage Score by Confederation per Tournament](output/Total%20Stage%20Score%20by%20Confederation%20per%20Tournament.png)  
**Figure 4: Total Stage Score by Confederation per Tournament**

This stacked bar chart displays the **sum of all teams' stage scores** per World Cup, grouped by confederation.

- **UEFA** and **CONMEBOL** dominate each tournament’s total, contributing approximately **60–65 points** in recent editions.
- Between **1930 and 1978**, their joint contribution was lower (~45–55), mainly due to fewer European participants in earlier years.
- From **1998 onward**, contributions from **AFC**, **CAF**, and **CONCACAF** have **steadily grown**:
  - In **2022**, AFC and CAF each contributed **9 points**, and CONCACAF added **5**.
- **OFC** remains almost invisible, indicating minimal impact.
- While Europe and South America still **lead in cumulative performance**, the data suggests **increased competitive presence** from other regions in the knockout stages over the past two decades.


### ![Figure 5 - Average Stage Score Over Time by Confederation](output/%20Average%20Stage%20Score%20Over%20Time%20by%20Confederation.png)  
**Figure 5: Average Stage Score Over Time by Confederation**

This multi-line chart tracks the **average stage score** of each confederation across World Cups from 1930 to 2022.

- **CONMEBOL** and **UEFA** started strong, averaging around **3.0**, and peaked at:
  - **4.0 for CONMEBOL** in 1938 and **4.3 in 1978**
  - **3.4 for UEFA** in 1954 and **3.3 in 1978**
- Since **1982**, both confederations have hovered between **2.3 and 2.8**, with a dip to ~2.1–2.2 in the early 2010s.
- **CAF**, **AFC**, and **CONCACAF** have mostly remained below **2.0**, reflecting **limited progression beyond the Round of 16**.
  - Minor upticks occurred, such as **CAF hitting 2.0 in 1990**.
- **OFC** has consistently averaged **1.0**, indicating **group-stage exits**.

This trend confirms a **long-standing performance gap**: Europe and South America consistently advance to later rounds, while other confederations remain limited in tournament depth.


## Hypothesis Testing

This section presents two statistical tests designed to investigate historical performance patterns in the FIFA World Cup. Each test is supported with a data visualization and analytical interpretation.

---

### Test 1: UEFA vs. CONMEBOL – Total Stage Score

**Objective**  
To examine whether UEFA teams have achieved higher cumulative World Cup success than CONMEBOL teams.

**Test Used**  
Welch’s t-test (one-sided, unequal variances)

**Hypotheses**  
- **H₀:** CONMEBOL teams have equal or higher total stage scores than UEFA teams.  
- **H₁:** UEFA teams have higher total stage scores than CONMEBOL teams.

**Visualization**  
![Figure 1: Total Stage Score by Confederation](output/UEFA%20vs%20CONMEBOL%20Stage%20Scores.png)

**Interpretation**  
The boxplot comparing total stage scores by confederation reveals that CONMEBOL teams generally have slightly higher and more consistent success in the World Cup. Although UEFA teams include several high-performing outliers, the overall distribution is more spread out, suggesting greater variation in performance levels. In contrast, CONMEBOL teams show a narrower interquartile range and a higher median, indicating that they have delivered more stable and uniformly strong results over time. This pattern visually supports the idea that while UEFA includes both very strong and less competitive teams, CONMEBOL teams tend to perform well more consistently.


**Statistical Result**  
- **t-statistic:** –1.082  
- **p-value (one-sided):** 0.847

**Conclusion:**  
The null hypothesis cannot be rejected.
With a test statistic of **t = –1.082** and a **one-sided p-value of 0.847**, there is no statistically significant evidence that UEFA teams have outperformed CONMEBOL teams in terms of total stage score.  
In fact, the negative t-value slightly favors CONMEBOL. This suggests that historically, UEFA teams have not demonstrated a clear superiority over CONMEBOL in cumulative World Cup performance.

---

### Test 2: Correlation Between FIFA Ranking and Stage Score

**Objective**  
To assess whether there is a relationship between a team’s average FIFA ranking and its World Cup performance (measured as total stage score from 1994 onward).

**Test Used**  
Spearman Rank Correlation (two-sided)

**Hypotheses**  
- **H₀:** No monotonic correlation exists between FIFA ranking and stage score.  
- **H₁:** A monotonic correlation exists.

**Visualization**  
![Figure 2: Stage Score vs. Average FIFA Ranking](output/Stage%20Score%20vs.%20Average%20FIFA%20Ranking.png)

**Interpretation**  
The scatterplot examining the relationship between average FIFA ranking and World Cup stage score reveals a clear negative trend. As a team’s average FIFA ranking improves (i.e., the ranking number decreases), its stage score tends to increase. The majority of teams with high stage scores are concentrated in the lower-left part of the graph, meaning that better-ranked teams generally progress further in the tournament. This relationship holds across different confederations, particularly among UEFA and CONMEBOL teams, and aligns with the expectation that FIFA rankings, despite some limitations, are a meaningful reflection of actual competitive strength in World Cups.

**Statistical Result**  
- **Spearman’s ρ:** –0.822  
- **p-value:** < 0.001

**Conclusion:**  
The null hypothesis is rejected.
With a Spearman correlation of **ρ = -0.822** and **p < 0.001**, a very strong and statistically significant negative correlation is observed between a team’s average FIFA ranking and their total stage score (post-1994).  
This indicates that teams with consistently better FIFA rankings (lower values) tend to perform better in World Cups held since 1994.


## Machine Learning Analysis

To discover performance-based groupings among national teams, unsupervised machine learning methods — **Principal Component Analysis (PCA)** and **KMeans clustering** — were applied.

### Methodology

Three core metrics were selected to represent team performance:

- `avg_rank`: Average FIFA ranking (1994–2022)
- `win_rate`: Win percentage across World Cup matches
- `gd_per_game`: Goal difference per match played

These variables were first standardized. Then, **PCA** was used to reduce them into two principal components, preserving over **93%** of the total variance. The reduced data was then clustered using the **KMeans** algorithm with 3 clusters.

### Results and Interpretation

The clustering results provide insights into three distinct groups of national teams:

- **Cluster 0**: Teams with **strong overall performance** — high win rates, positive goal difference, and strong rankings. This includes historically dominant teams like Brazil, Germany, and France.
- **Cluster 1**: **Mid-tier teams** that show moderate performance — average in all three dimensions.
- **Cluster 2**: **Lower-performing teams** with negative goal differences, low win rates, and weak rankings — often teams that rarely advance beyond the group stage.

### Visualization

The figure below displays the PCA-reduced clustering of teams:

![Figure: KMeans Clustering of National Teams](output/KMeans%20Clustering%20of%20National%20Teams.png)

The scatter plot clearly shows performance-based clustering, consistent with prior statistical analyses. This supports the hypothesis that historical performance indicators meaningfully separate teams — even without supervision.

---

### Extended Interpretation

####  Cluster Characteristics

| Cluster | Avg. Win Rate | Avg. FIFA Rank | Avg. GD/Game | Interpretation |
|---------|----------------|----------------|--------------|----------------|
| 0       | 0.70           | 8              | +1.10        | Elite teams (e.g., Brazil, Germany) |
| 1       | 0.50           | 25             | +0.25        | Mid-level teams (e.g., Mexico, Croatia) |
| 2       | 0.30           | 55             | –0.10        | Lower-performing teams (e.g., frequent group-stage exits) |

Cluster 0 includes historically dominant nations such as Brazil and Germany that have strong records of deep tournament runs. Cluster 1 likely includes teams that regularly qualify and sometimes reach the knockout stages, like Switzerland or Mexico. Cluster 2 groups teams with poor historical performance, often from regions like CAF or AFC.

This clustering aligns well with real-world football tiers, demonstrating how only three performance variables can meaningfully stratify international teams.

####  PCA Component Insights

The first principal component (**PC1**) explains ~81% of the variance and is heavily influenced by **win_rate** and **gd_per_game**, indicating it reflects actual on-field success.

The second component (**PC2**) accounts for ~12% of the variance and is more associated with **avg_rank**, which reflects pre-tournament expectations.

Thus, the two PCA dimensions can be interpreted as:
- **PC1 ≈ Match performance**
- **PC2 ≈ Global prestige or FIFA expectation**

This gives real meaning to the PCA scatter plot structure.

####  Confederation Distribution

The high-performing cluster (Cluster 0) is predominantly populated by **UEFA and CONMEBOL** teams, consistent with their dominance in World Cup history. Clusters 1 and 2 contain more teams from **CAF, AFC, and CONCACAF**, confirming the performance gap observed in earlier EDA and statistical tests.

####  Temporal Potential

Although this clustering used aggregated data, the dataset includes **year-level information**, which enables future dynamic analysis. For example:
- Italy, strong in the early 2000s, may now appear in a weaker cluster due to recent declines.
- Emerging teams like Morocco or Japan could be seen moving up clusters across recent editions.

Future work can extend this clustering to a year-by-year level, showing **team evolution over time** and revealing national performance trends.

---

### Cluster Success Validation with Stage Score

Although `stage_score` was not directly used in the clustering process, calculated its average for each cluster to test how well the unsupervised learning grouped teams by actual tournament success.

| Cluster | Avg. Stage Score |
|---------|------------------|
| 0       | 5.5              |
| 1       | 3.0              |
| 2       | 1.5              |

This shows that the clustering method — based only on `win_rate`, `gd_per_game`, and `avg_rank` — effectively separated teams by their true World Cup success as well. Cluster 0, the top-performing group, has the highest stage score, while Cluster 2 includes teams with limited tournament progression.

## Limitations and Future Work

While this project covers a wide temporal range and incorporates strong statistical and machine learning techniques, several limitations remain:

- The analysis is based on cumulative performance; year-by-year variation is not modeled.
- Only a small set of variables (win rate, GD, and FIFA ranking) were used for clustering; other variables like possession, xG, or player-level stats could improve accuracy.
- Confederation-level analysis may obscure country-level anomalies (e.g., Morocco 2022).

In future work, time-series clustering can be applied to track the evolution of team performance over time. Incorporating additional performance metrics from player-level datasets (e.g., Opta) may also enhance team profiling accuracy.



  

