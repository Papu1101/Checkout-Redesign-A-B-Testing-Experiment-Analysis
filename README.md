# Checkout-Redesign-A-B-Testing-Experiment-Analysis
A portfolio-grade A/B testing analysis of an e-commerce checkout redesign. Evaluates conversion, AOV, revenue per user, device-level treatment effects, statistical significance, confidence intervals, and revenue impact to identify performance differences and recommend a data-driven change &amp; retest strategy.
# 🛒 Checkout Experiment Analytics — A/B Testing & Revenue Impact

## 📌 Project Overview

This project analyzes a four-week **A/B test for an e-commerce checkout redesign**, comparing the existing checkout experience (**Control**) with a redesigned experience (**Treatment**).

The analysis evaluates whether the redesigned checkout improves customer conversion and revenue while investigating whether its impact differs across **device types** and **visitor segments**.

The project follows an end-to-end experimentation workflow covering **data integrity, metric definition, statistical testing, segmentation, interaction analysis, and revenue impact estimation**.

---

## 🎯 Business Problem

An e-commerce company introduced a redesigned checkout experience and ran a randomized experiment to determine whether the new experience improves customer purchasing behavior.

The key business questions were:

* Does the redesigned checkout increase conversion?
* Is the observed improvement statistically significant?
* Does the redesign affect **AOV** and **revenue per user**?
* Does performance differ across desktop, mobile, and tablet users?
* Does the treatment behave differently for new and returning visitors?
* What is the potential monthly revenue impact?
* Should the redesigned checkout be launched, modified, or retested?

---

## 📊 Experiment Design

| Component                  | Description                    |
| -------------------------- | ------------------------------ |
| Experiment                 | Checkout Redesign A/B Test     |
| Duration                   | September 2025                 |
| Control                    | Existing checkout experience   |
| Treatment                  | Redesigned checkout experience |
| Initial Assignment Records | 31,284                         |
| Unique Users               | 31,000                         |
| Clean Experiment Users     | 30,716                         |
| Orders                     | 2,670                          |
| Primary Metric             | User conversion rate           |
| Secondary Metrics          | AOV, Revenue per User          |
| Segments                   | Device, Visitor Type           |

---

## 🧹 Experiment Integrity & Data Quality

Before calculating experiment metrics, the assignment and order data were validated to ensure that treatment effects could be attributed correctly.

### Assignment Integrity

The assignment dataset contained:

* **31,284 assignment records**
* **31,000 unique users**
* **284 users assigned to both Control and Treatment**
* **568 assignment records associated with mixed-variant users**

Because users appeared in both experiment variants, these **284 users were excluded from the primary analysis** to prevent treatment contamination.

After cleaning:

* **30,716 eligible users**
* **15,339 Control**
* **15,377 Treatment**
* Approximately **50/50 experiment split**

### Order Attribution

Order records were also checked for:

* Duplicate order IDs
* Missing timestamps
* Invalid order values
* Orders from users outside the experiment
* Orders occurring before assignment
* Orders associated with mixed-variant users

A total of **104 orders** were excluded from primary attribution because they were associated with mixed users and/or occurred before valid assignment.

The final analysis used **2,560 valid post-assignment orders**.

---

## 📈 Primary Metric — Conversion Rate

The primary metric was defined as:

> **Percentage of assigned users who placed at least one order after assignment.**

| Variant   |  Users | Converted Users | Conversion |
| --------- | -----: | --------------: | ---------: |
| Control   | 15,339 |           1,113 |      7.26% |
| Treatment | 15,377 |           1,185 |      7.71% |

### Treatment Effect

* Absolute improvement: **+0.45 percentage points**
* Relative lift: **+6.21%**

The treatment group showed a higher observed conversion rate.

However, statistical testing was required to determine whether this difference could reasonably be attributed to the experiment rather than sampling variation.

---

## 🧪 Statistical Significance

A two-proportion z-test was used to compare conversion rates between Control and Treatment.

### Hypotheses

**H₀:** Control and Treatment have the same conversion rate.

**H₁:** Control and Treatment have different conversion rates.

### Results

| Statistic             |               Result |
| --------------------- | -------------------: |
| Z-statistic           |               1.4998 |
| p-value               |               0.1337 |
| Significance level    |                 0.05 |
| 95% CI for difference | −0.14 pp to +1.04 pp |

The confidence interval includes zero and the p-value is above 0.05.

Therefore, the observed **+0.45 percentage-point conversion improvement was not statistically significant at the 5% level**.

---

## 💰 Revenue & Monetization Analysis

### Average Order Value

| Variant   |    Revenue | Orders |    AOV |
| --------- | ---------: | -----: | -----: |
| Control   | $78,740.25 |  1,240 | $63.50 |
| Treatment | $85,232.21 |  1,320 | $64.57 |

Observed AOV improvement:

**+1.68%**

---

### Revenue Per User

Revenue per user was calculated across the full eligible experiment population, including users with no orders.

| Variant   | Revenue per User |
| --------- | ---------------: |
| Control   |            $5.13 |
| Treatment |            $5.54 |

Observed RPU lift:

**+7.98%**

A Welch's t-test was used to compare user-level revenue.

* Difference: **+$0.41 per user**
* t-statistic: **1.7013**
* p-value: **0.0889**
* 95% CI: **−$0.06 to +$0.88**

The RPU difference was therefore **not statistically significant at the 5% level**.

---

## 📱 Device-Level Analysis

The experiment showed substantially different results across device types.

| Device  | Control | Treatment | Difference |
| ------- | ------: | --------: | ---------: |
| Desktop |   7.53% |    10.11% |   +2.58 pp |
| Mobile  |   7.07% |     5.42% |   −1.66 pp |
| Tablet  |   6.61% |     5.10% |   −1.51 pp |

The desktop experience showed a strong positive treatment effect, while mobile and tablet users showed lower conversion under Treatment.

---

## 🔬 Multiple-Testing Correction

Separate statistical tests were performed for the device segments and visitor-type segments.

Because multiple segment tests increase the probability of false positives, **Benjamini-Hochberg False Discovery Rate correction** was applied.

After correction:

* Desktop: statistically significant
* Mobile: statistically significant
* Tablet: not statistically significant
* New visitors: not statistically significant
* Returning visitors: not statistically significant

Segment-level significance was not treated as sufficient evidence of treatment heterogeneity; an explicit interaction model was used to test that question.

---

## 🔄 Treatment × Device Interaction

A logistic regression model was used to directly test whether the treatment effect differed by device:

```text
Converted ~ Variant × Device
```

Desktop was used as the reference category.

### Interaction Results

| Interaction        | Coefficient | p-value |
| ------------------ | ----------: | ------: |
| Treatment × Mobile |     −0.6072 |  <0.001 |
| Treatment × Tablet |     −0.5985 |   0.001 |

Both interaction terms were statistically significant.

### Interpretation

The results provide evidence that the treatment effect **varied significantly by device**.

The redesigned checkout performed substantially differently on mobile and tablet compared with desktop.

This is an important finding because the overall experiment result can mask meaningful differences in user experience across devices.

---

## 👥 Visitor-Type Analysis

The experiment was also evaluated across new and returning visitors.

| Visitor Type | Control | Treatment | Difference |
| ------------ | ------: | --------: | ---------: |
| New          |   6.10% |     6.20% |   +0.10 pp |
| Returning    |   9.15% |    10.22% |   +1.07 pp |

Neither visitor-type comparison remained statistically significant after accounting for multiple comparisons.

---

## 💵 Estimated Monthly Revenue Impact

The observed RPU difference was used to estimate potential incremental revenue.

### Point Estimate

**+$12,578/month**

### Estimated Range

Using the 95% confidence interval for RPU:

* Lower bound: **−$1,913/month**
* Point estimate: **+$12,578/month**
* Upper bound: **+$27,069/month**

This range illustrates the uncertainty around the revenue estimate rather than representing guaranteed financial impact.

---

## 🧠 Key Findings

### 1. Conversion increased, but evidence was inconclusive

Treatment conversion was **7.71% vs. 7.26%** for Control, representing a **+6.21% relative lift**.

However, the difference was not statistically significant.

### 2. Revenue metrics showed positive point estimates

Treatment produced higher observed AOV and RPU.

However, the RPU difference was also not statistically significant at the 5% level.

### 3. Device type was a major source of treatment heterogeneity

The interaction analysis found statistically significant differences between the treatment effect on desktop versus mobile and tablet.

### 4. Visitor type did not show statistically significant treatment differences

New and returning visitors showed positive point estimates, but the differences were not statistically significant after multiple-testing correction.

### 5. Revenue impact remains uncertain

The point estimate suggests approximately **$12.6K in incremental monthly revenue**, but the estimated range extends from approximately **−$1.9K to +$27.1K**.

---

## 🚦 Final Recommendation

### **Change & Retest**

The redesigned checkout should **not be rolled out universally in its current form** based solely on this experiment.

The primary conversion metric showed a positive point estimate, but the improvement was not statistically significant. Revenue metrics were also directionally positive but uncertain.

The strongest finding was the significant **Treatment × Device interaction**, with materially different treatment effects across desktop, mobile, and tablet.

### Recommended Next Steps

1. Investigate mobile and tablet checkout behavior.
2. Identify device-specific friction or technical issues.
3. Preserve successful elements of the desktop redesign.
4. Develop an improved mobile/tablet checkout experience.
5. Run a follow-up randomized A/B test.
6. Predefine the primary hypothesis and success criteria.
7. Continue tracking conversion, AOV, RPU, and revenue impact.
8. Pre-specify device-level interaction analysis for the next experiment.

---

## 🛠️ Tools & Technologies

* **Python**
* **Pandas**
* **NumPy**
* **SciPy**
* **Statsmodels**
* **Matplotlib**
* **Seaborn**
* **Jupyter Notebook**
* **Statistical Hypothesis Testing**
* **Logistic Regression**
* **A/B Testing**
* **Experiment Design**
* **Revenue Impact Analysis**

---

## 📂 Project Structure

```text
checkout-experiment-analytics/
│
├── Checkout_AB_Testing.ipynb
├── README.md
│
├── data/
│   └── README.md
│
└── images/
    ├── conversion_analysis.png
    ├── device_analysis.png
    └── revenue_impact.png
```

> Raw experiment data may be excluded from the repository where appropriate.

---

## 📌 Skills Demonstrated

**Data Analytics:**
Data Cleaning · EDA · Data Validation · Feature Engineering

**Experimentation:**
A/B Testing · Experiment Integrity · Conversion Analysis · Statistical Testing · Confidence Intervals

**Statistics:**
Hypothesis Testing · Proportion Tests · Welch's t-test · Multiple-Testing Correction · Interaction Effects

**Business Analytics:**
Revenue Impact · AOV · Revenue per User · Segmentation · Business Recommendations

**Python:**
Pandas · NumPy · SciPy · Statsmodels · Matplotlib · Seaborn

---

## 📊 Project Outcome

This project demonstrates an end-to-end approach to analyzing an A/B test beyond simply comparing two percentages.

The analysis combines **experiment quality checks, statistical inference, segmentation, interaction modeling, and financial impact estimation** to translate experimental data into a practical product decision.
