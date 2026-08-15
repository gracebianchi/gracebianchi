# Hi there, I'm Grace Bianchi

I'm a rising senior at UC Santa Barbara double-majoring in Statistics & Data Science (B.S.) and Economics (B.A.), with a quantitative foundation built through coursework in econometrics, machine learning, and stochastic processes. 

[Resume](https://github.com/gracebianchi/gracebianchi/blob/main/Grace%20Bianchi%20Resume.pdf) | [LinkedIn](http://www.linkedin.com/in/gracefbianchi) | gracefbianchi@gmail.com

## Recent Experience

### Data Quality and Solutions Summer Analyst - MUFG - Summer 2026

Interned on the Data Quality and Solutions team at MUFG, one of the world's largest financial groups, where I worked at the intersection of data engineering and risk analytics. I built a Python and PostgreSQL pipeline to extract and structure a decade of loss-run data, then modeled claim frequency and severity distributions with Monte Carlo simulation to quantify exceedance risk, work that directly supported a coverage reduction saving $250K in premiums. I also validated financial-crimes detection logic in SQL during a legacy-to-new platform migration, ensuring rule parity at an institutional scale.

## Languages

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Java](https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=openjdk&logoColor=white)
![R](https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Stata](https://img.shields.io/badge/Stata-1A5276?style=for-the-badge&logo=stata&logoColor=white)

## Libraries & Tools

![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=python&logoColor=white)
![tidyverse](https://img.shields.io/badge/tidyverse-1A162D?style=for-the-badge&logo=r&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)

## Projects

### [SPY Markov Regime-Switching Volatility Forecaster](https://github.com/gracebianchi/volatility-forecaster) 

Built a multi-stage volatility forecasting system for SPY, progressing from classical models (EWMA, GARCH, HAR-RV) through machine learning extensions to a full Markov regime-switching framework with formal risk-management backtesting. The project's central question shifts at each stage, from "which model forecasts volatility best" to "does modeling volatility regimes actually improve risk management," and is evaluated accordingly, with Stage 1 judged on forecast RMSE and Stage 2 on VaR/ES tail-risk accuracy. It now runs as a live daily forecaster via a GitHub Actions pipeline that pulls fresh market data automatically, with a planned extension to write its outputs to AWS S3.

- Benchmarked EWMA, GARCH(1,1), and HAR-RV on a chronological train/test split (2015-2022 vs. 2023+) and found HAR-RV performed best (RMSE 4.90 vs. 7.39 and 8.70), then confirmed with a linear regression model (test RMSE 4.87) that HAR-RV's fixed-lag structure was already capturing nearly all of the linearly forecastable signal in realized volatility
- Fit a 4-state Gaussian HMM (Calm/Normal/Stressed/Panic) on log realized volatility, selected via BIC, and built a regime-conditional Markov-Switching HAR; a Diebold-Mariano test on the QLIKE loss differential (DM = 0.94, p = 0.35) showed the regime model's edge over single-regime HAR was directionally present but not statistically significant on point forecasts alone
- Converted both the single-regime and regime-switching forecasts into 99%/95% VaR and Expected Shortfall using a conditional Generalized Pareto tail fit, and backtested with Kupiec and Christoffersen coverage tests; both specifications passed cleanly at both confidence levels (all p > 0.05), showing that EVT-based tail modeling, not regime-awareness itself, was what fixed the calibration a Gaussian tail assumption couldn't achieve
- Built a Monte Carlo path simulator for regime-aware fan-chart forecasts and deployed the full pipeline as a live daily SPY forecaster via GitHub Actions, with an in-progress extension to persist daily outputs to AWS S3

### [Stellar Classification: Using Machine Learning to Assess the Role of Redshift](https://github.com/gracebianchi/Stellar_Classification_Model)

Built and compared seven classification models (Random Forest, Boosted Tree, Elastic Net, Decision Tree, KNN, LDA, and QDA) across two feature sets to classify celestial objects as stars, galaxies, or quasars, using a 5,000-observation sample drawn from the full 100,000-record SDSS dataset to keep training and tuning computationally manageable. The core objective was to test whether photometric filter measurements alone are sufficient for classification, or whether spectroscopic redshift is necessary to achieve strong performance.

- Achieved a 0.996 ROC AUC and 97.9% test accuracy with a Random Forest model when redshift was included, with the top four of seven models (Random Forest, Boosted Tree, Elastic Net, Decision Tree) all exceeding 0.99 ROC AUC
- Quantified redshift's predictive value directly: removing it dropped Random Forest's ROC AUC from 0.996 to 0.931 and accuracy from 97.9% to 84.1%, a ~14-point accuracy decline that confirms redshift carries information the five photometric filters can't fully replace
- Used confusion matrix analysis to show the redshift-free model's error wasn't uniform: nearly 39% of true stars were misclassified once redshift was removed, isolating STAR as the class most dependent on that feature
- Addressed class imbalance (galaxies made up ~59% of the sample) by using stratified 10-fold cross-validation and prioritizing ROC AUC over raw accuracy as the primary evaluation metric, since a naive always-predict-galaxy model would already score ~59% accuracy

### [Factorial ANOVA: Testing Design and Mass Effects on Flight Distance](https://github.com/gracebianchi/flight-distance-anova)

Designed and ran a controlled 2×4 factorial experiment testing how airplane structure (4 designs) and added nose mass (paperclip on/off) affect paper airplane flight distance, with full randomization of throw order to control for bias and thrower fatigue. The project's objective was to formally test whether design and mass each independently affect flight performance, and whether the two factors interact, using two-way ANOVA on log-transformed distance data.

- Found significant effects of design (p = 3.32e-06), added mass (p = 7.72e-05), and a significant design-by-mass interaction (p = 0.000111), meaning the effect of adding weight genuinely depends on the airplane's structure rather than acting uniformly
- Used Tukey's HSD post-hoc test to show the interaction was directional, not just statistically present: adding a paperclip boosted Design B's average distance from 187 to 224 inches, while it hurt Design D's, dropping it from 165 to 136 inches
- Validated all two-way ANOVA assumptions before trusting the result: applied a log transformation to correct right-skew, then confirmed residual normality via Shapiro-Wilk (p = 0.858) and homogeneity of variance via Bartlett's test (p = 0.366)
- Controlled for confounding through experimental design itself, not just statistics: randomized throw order across all 64 trials and balanced throws evenly across three team members to isolate the effects of design and mass from thrower-specific variation

### [Housing Market Segmentation Using Clustering and Association Rules](https://github.com/gracebianchi/Cluster-Analysis-and-Association-Rules-House-Prices)

Applied k-means, hierarchical clustering, PAM, and association rule mining to a dataset of 1,047 houses to identify natural groupings in the housing market and the feature combinations most strongly tied to price. The project cross-validates the cluster structure across multiple algorithms and pairs it with market-basket-style analysis to surface interpretable pricing rules.

- Identified a consistent 3-cluster structure via k-means (budget/aging homes, mid-range homes, and large high-value homes) that was independently confirmed by hierarchical clustering and PCA, with the first principal component (49% of variance) cleanly capturing a size-value axis across living area, lot size, price, and bedroom/bathroom count
- Validated cluster robustness across methods: a Hopkins statistic of 0.999 confirmed genuine cluster tendency in the data, and PAM's silhouette analysis converged on a complementary 2-cluster view (broad low- vs. high-value split) that reconciled cleanly with k-means' more granular 3-cluster segmentation
- Mined 6,749 association rules via Apriori and found that small, one-bathroom, mid-aged homes on small lots predict a two-bedroom layout with 94% confidence (lift ~5.6), while large living area, 3+ bathrooms, and large lots predict the expensive price tier with 100% confidence (lift ~2.94)
- Compared four hierarchical linkage methods by cophenetic correlation and selected Ward.D2 despite its lower distance-preservation score (0.52 vs. 0.76 for average linkage), prioritizing its more compact, interpretable clusters and closer alignment with the k-means partition

### [Economic Freedom Index (2019): Exploratory Data Analysis & Correlation Study](https://github.com/gracebianchi/EDA_Economic_Freedom_Index)

Analyzed the 2019 Economic Freedom Index across 186 countries to understand which institutional, economic, and social factors are most closely tied to a nation's level of economic freedom. The project combines distribution analysis, correlation testing, and regional/categorical comparisons to identify the strongest drivers of economic freedom and their interactions with wealth and governance.

- Found property rights (r = 0.83), judicial effectiveness (r = 0.81), and government integrity (r = 0.80) to be the strongest correlates of economic freedom, well above GDP per capita (r = 0.64), pointing to institutional quality as a stronger driver than raw wealth
- Identified a bimodal distribution in property rights scores, revealing two distinct global clusters of countries rather than a smooth continuum of institutional strength
- Compared the five highest- and five lowest-scoring countries (Hong Kong and Singapore vs. North Korea and Venezuela) directly across property rights, trade freedom, and business freedom to isolate what structurally separates the two groups
- Found essentially no relationship between GDP growth rate or population size and economic freedom, showing that short-term growth and country size don't meaningfully predict institutional quality

<!--
**gracebianchi/gracebianchi** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:[Resume July 2025-Grace Bianchi (2).docx (1).pdf](https://github.com/user-attachments/files/21975082/Resume.July.2025-Grace.Bianchi.2.docx.1.pdf)


- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
