# 📊 Causal Inference with Sharp & Fuzzy Regression Discontinuity Designs

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-Statistical%20Modeling-4051B5?style=for-the-badge)
![Linearmodels](https://img.shields.io/badge/Linearmodels-IV%20%2F%202SLS-8A2BE2?style=for-the-badge)
![Causal Inference](https://img.shields.io/badge/Causal-Inference-FF6F00?style=for-the-badge)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

</p>

---

# 📖 Project Overview

This project demonstrates the application of **Regression Discontinuity Design (RDD)** as a causal inference technique for estimating treatment effects in observational or quasi-experimental settings.

The central idea behind RDD is that when treatment assignment is determined by whether an observable **running variable** crosses a predefined cutoff, observations immediately on either side of that threshold can be compared to estimate a causal effect.

The notebook implements two important variants of RDD:

- 🔵 **Sharp Regression Discontinuity Design (Sharp RDD)**
- 🟠 **Fuzzy Regression Discontinuity Design (Fuzzy RDD)**

The Sharp RDD example studies the relationship between **age and all-cause mortality around the age-21 cutoff**, while the Fuzzy RDD example evaluates a **tutoring program assigned around an entrance-exam threshold**.

The project also demonstrates how **quadratic terms, bandwidth selection, heteroskedasticity-robust standard errors, Instrumental Variables (IV), and Two-Stage Least Squares (2SLS)** can be incorporated into causal analysis.

---

# 🎯 Aim

The primary objectives of this project are to:

- Understand Regression Discontinuity Designs as a causal inference method.
- Estimate treatment effects using a clearly defined cutoff.
- Understand the difference between **Sharp and Fuzzy RDD**.
- Model non-linear relationships around the treatment threshold.
- Explore the effect of different bandwidths around the cutoff.
- Understand the importance of robust standard errors.
- Examine whether other variables also change at the cutoff.
- Understand why naive OLS can be biased in a Fuzzy RDD setting.
- Use **Instrumental Variables (IV)** to address treatment non-compliance.
- Implement **Two-Stage Least Squares (2SLS)**.
- Estimate the **Local Average Treatment Effect (LATE)** near the cutoff.

---

# 💡 What is Regression Discontinuity?

Regression Discontinuity Design is a quasi-experimental method used when treatment assignment depends on a threshold.

For example:

```text
                 Cutoff
                   │
                   ▼
─────────────── 21 ───────────────
     Control         Treatment
```

Instead of comparing completely different groups, RDD focuses on observations **close to the cutoff**.

The basic intuition is:

> If observations just below and just above the threshold are sufficiently similar, a sudden change in the outcome at the cutoff can provide evidence of a causal treatment effect.

This makes RDD especially useful when randomized experiments are difficult or impossible to conduct.

---

# ✨ Project Highlights

✅ Regression Discontinuity Design

✅ Sharp RDD

✅ Fuzzy RDD

✅ Cutoff-Based Treatment Assignment

✅ Running Variable Centering

✅ Exploratory Visualization

✅ Linear RDD Modeling

✅ Quadratic RDD Modeling

✅ Interaction Terms

✅ Bandwidth Analysis

✅ Heteroskedasticity-Robust Standard Errors

✅ Instrumental Variables (IV)

✅ Two-Stage Least Squares (2SLS)

✅ Local Average Treatment Effect (LATE)

✅ Causal Effect Estimation

---

# 🔵 Sharp Regression Discontinuity Design

The first part of the notebook implements a **Sharp RDD** using an age-based treatment threshold.

The running variable is:

```text
Age
```

and the treatment assignment changes at:

```text
Age = 21
```

The notebook creates:

```text
Treatment → Age ≥ 21

Control   → Age < 21
```

The running variable is then centered around the cutoff:

```text
Age_centered = Age - 21
```

The outcome variable is **all-cause mortality**, allowing the model to investigate whether there is a discontinuous change around the age-21 threshold.

---

# 📈 Sharp RDD Modeling

The project begins with a simple linear specification:

```text
Outcome = Intercept
        + Treatment
        + Centered Age
        + Error
```

A more flexible specification is then introduced by including:

- Treatment × Age interaction
- Quadratic Age terms
- Quadratic terms interacted with Treatment

This allows the relationship between age and the outcome to vary more flexibly on either side of the cutoff.

---

# 🧮 Why Add Quadratic Terms?

A purely linear model assumes that the relationship between the running variable and outcome follows a straight line.

However, the relationship may be curved.

Therefore, the project introduces terms such as:

```text
Age²
```

and interactions involving the treatment group.

This gives the regression greater flexibility when estimating the relationship around the cutoff.

---

# 📏 Bandwidth Analysis

A key concept in RDD is **bandwidth**.

Instead of using the entire dataset, observations close to the cutoff can be analyzed separately.

Conceptually:

```text
Entire Dataset

──────────────────────────────────────────────
                 │
              Cutoff
                 │
──────────────────────────────────────────────


Local Bandwidth

          ◄──────┼──────►
               Cutoff
```

The notebook examines observations in a narrower region around the cutoff and compares the resulting estimates.

This demonstrates an important trade-off:

- Wider bandwidth → More observations, potentially more bias from observations far from the cutoff.
- Narrower bandwidth → More local comparison, but fewer observations and potentially larger standard errors.

---

# 🛡️ Robust Standard Errors

The regression models use **HC1 heteroskedasticity-robust standard errors**.

This helps make statistical inference more reliable when the variance of the regression errors may not be constant.

---

# 🧪 RDD Validity Checks

The notebook also highlights an important RDD diagnostic:

> **Do other variables also jump at the cutoff?**

If unrelated variables show a discontinuity at exactly the same threshold, it may suggest that the estimated treatment effect is capturing something other than the treatment itself.

Therefore, checking for discontinuities in other variables is an important part of validating the RDD design.

---

# 🟠 Fuzzy Regression Discontinuity Design

The second part of the project introduces **Fuzzy RDD**.

Unlike Sharp RDD, crossing the cutoff does **not perfectly determine treatment**.

Instead, crossing the threshold changes the **probability of receiving treatment**.

The project uses a **tutoring program** example where eligibility is determined by an entrance-exam cutoff.

The running variable is:

```text
Entrance Exam Score
```

with a cutoff at:

```text
Entrance Exam = 70
```

The treatment is:

```text
Tutoring
```

and the outcome is:

```text
Exit Exam Score
```

---

# 🔀 Sharp vs Fuzzy RDD

| Sharp RDD | Fuzzy RDD |
|-----------|-----------|
| Cutoff determines treatment directly | Cutoff changes probability of treatment |
| Treatment assignment is deterministic | Treatment assignment is imperfect |
| Direct discontinuity interpretation | Requires an IV approach |
| Treatment = threshold-based assignment | Eligibility = instrument |

This distinction is one of the major concepts demonstrated in the project.

---

# ⚠️ Why Naive OLS Can Be Biased

In the tutoring example, simply estimating:

```text
Exit Exam ~ Tutoring + Entrance Score
```

can produce a biased estimate because students may not perfectly comply with the treatment assignment rule.

Some eligible students may not participate, while some ineligible students may receive treatment.

Therefore, treatment participation is **endogenous**, creating the need for an instrumental-variable approach.

---

# 🎯 Instrumental Variables

The Fuzzy RDD uses **eligibility at the cutoff as an instrument** for actual tutoring participation.

The instrument is represented as:

```text
V = 1 if Entrance Exam < 70
V = 0 otherwise
```

Conceptually:

```text
Eligibility at Cutoff
          │
          ▼
      Tutoring
          │
          ▼
    Exit Exam Score
```

The cutoff-based eligibility provides an external source of variation that can be used to estimate the causal effect of tutoring.

---

# 🧠 Two-Stage Least Squares (2SLS)

The project implements **IV2SLS** using the `linearmodels` library.

The approach can be understood in two stages:

### Stage 1

Predict treatment participation using the instrument:

```text
Tutoring ← Eligibility + Entrance Score
```

### Stage 2

Use the predicted treatment to estimate its effect on the outcome:

```text
Exit Exam ← Predicted Tutoring + Entrance Score
```

The final estimate represents the local causal effect of tutoring for observations influenced by the cutoff.

---

# 📊 Local Average Treatment Effect (LATE)

The Fuzzy RDD / IV approach estimates a **Local Average Treatment Effect (LATE)**.

LATE represents the causal effect for the subgroup whose treatment status is influenced by the cutoff-based instrument.

This makes the interpretation different from a simple population-wide average treatment effect.

---

# ⚙️ Complete Workflow

```text
                 CAUSAL INFERENCE
                        │
                        ▼
                 Dataset Analysis
                        │
                        ▼
               Identify Cutoff
                        │
          ┌─────────────┴─────────────┐
          │                           │
          ▼                           ▼
       Sharp RDD                  Fuzzy RDD
          │                           │
          ▼                           ▼
   Define Treatment            Define Eligibility
      Threshold                   Threshold
          │                           │
          ▼                           ▼
  Center Running Variable      Center Running Variable
          │                           │
          ▼                           ▼
   Linear RDD Model             Naive OLS Model
          │                           │
          ▼                           ▼
  Quadratic RDD Model          Identify Non-Compliance
          │                           │
          ▼                           ▼
   Bandwidth Analysis              IV Setup
          │                           │
          ▼                           ▼
 Robust Standard Errors             2SLS
          │                           │
          ▼                           ▼
   RDD Interpretation              LATE
          │                           │
          └─────────────┬─────────────┘
                        ▼
               Causal Interpretation
```

---

# 🛠️ Tech Stack

| Category | Technologies |
|----------|--------------|
| Programming Language | Python |
| Data Manipulation | Pandas, NumPy |
| Statistical Modeling | Statsmodels |
| Instrumental Variables | Linearmodels |
| IV Estimation | IV2SLS / 2SLS |
| Visualization | Plotly |
| Development Environment | Jupyter Notebook |
| Data Format | Stata `.dta`, CSV |

---

# 📊 Results

The project demonstrates how **Regression Discontinuity Designs** can be used to estimate causal effects around externally defined thresholds.

### 🔵 Sharp RDD

The Sharp RDD analysis estimates the discontinuous change in the outcome around the age-21 cutoff using:

- Linear regression
- Quadratic specifications
- Treatment-group interactions
- Robust standard errors
- Narrower bandwidth analysis

This provides a framework for studying whether crossing the threshold is associated with a causal change in the outcome.

### 🟠 Fuzzy RDD

The Fuzzy RDD analysis demonstrates a more realistic setting where the cutoff affects **treatment eligibility rather than treatment participation perfectly**.

A naive OLS model is first considered, followed by an **Instrumental Variables / 2SLS approach** using the cutoff-based eligibility variable as an instrument.

The resulting framework estimates the **Local Average Treatment Effect (LATE)** around the cutoff.

---

# 🔍 Key Insights

The project demonstrates several important ideas in modern causal inference:

### 1. Causal effects can be estimated without randomized experiments

When treatment assignment follows a known threshold, observations near the cutoff can provide a quasi-experimental comparison.

### 2. Model specification matters

Linear and quadratic specifications can produce different fitted relationships, making functional-form choices important in RDD analysis.

### 3. Local analysis matters

Observations farther from the cutoff may not be as comparable as observations immediately around it.

### 4. Treatment compliance matters

In Fuzzy RDD, eligibility does not guarantee treatment, which requires an IV-based approach.

### 5. IV and 2SLS provide a solution to treatment endogeneity

The cutoff-based eligibility variable can act as an instrument for actual treatment participation.

---

# 📂 Repository Structure

```text
📦 Regression-Discontinuity-Causal-Inference
│
├── 📁 notebooks
│   └── Regression_Discontinuity.ipynb
│
├── 📁 data
│   └── tutoring_program_fuzzy.csv
│
├── 📁 images
│   ├── sharp_rdd_plot.png
│   ├── quadratic_rdd.png
│   ├── bandwidth_analysis.png
│   ├── fuzzy_rdd.png
│   └── treatment_effect.png
│
├── requirements.txt
├── LICENSE
└── README.md
```

---

# 🚀 Future Improvements

- Implement automated bandwidth selection.
- Compare multiple RDD bandwidth estimators.
- Add local polynomial regression.
- Perform placebo cutoff tests.
- Conduct manipulation / density tests around the cutoff.
- Add covariate balance checks.
- Implement additional IV estimators.
- Perform sensitivity analysis.
- Compare Sharp and Fuzzy RDD estimates visually.
- Apply RDD to a real-world policy or healthcare dataset.
- Extend the project toward modern causal machine learning.

---

# 🎓 Learning Outcomes

Through this project, you will gain practical experience in:

- Regression Discontinuity Design
- Sharp RDD
- Fuzzy RDD
- Running Variables
- Treatment Cutoffs
- Centering Variables
- Linear and Quadratic Specifications
- Interaction Terms
- Bandwidth Analysis
- Robust Standard Errors
- Causal Identification
- Instrumental Variables
- Two-Stage Least Squares
- Local Average Treatment Effect
- Quasi-Experimental Research Design
- Causal Inference using Observational Data

---

# 💼 Real-World Applications

Regression Discontinuity is widely useful when a real-world policy or decision uses a threshold.

Examples include:

### 🎓 Education

Studying the causal effect of scholarships, tutoring, or academic eligibility thresholds on student outcomes.

### 🏥 Healthcare

Evaluating medical treatment eligibility based on age, risk scores, or clinical thresholds.

### 💰 Economics

Measuring the effect of tax benefits, subsidies, or policy eligibility rules.

### 🏛️ Public Policy

Evaluating programs where eligibility is determined by an income, age, or test-score cutoff.

### 📊 Business

Analyzing the impact of credit limits, promotional eligibility, or customer segmentation thresholds.

---

# 📌 Project Significance

This project demonstrates a transition from **predictive machine learning toward causal and econometric reasoning**.

Traditional predictive modeling asks:

> **"Can we predict the outcome?"**

Causal inference asks:

> **"What is the effect of changing the treatment?"**

Regression Discontinuity provides a powerful framework for answering this question when treatment assignment is determined by a known threshold.

The inclusion of both **Sharp and Fuzzy RDD**, along with **Instrumental Variables and 2SLS**, makes this project particularly useful for understanding how modern causal analysis handles imperfect treatment assignment.

---

# 👨‍💻 Author

**Ambuj Tripathi**

🎓 Pre-Final Year B.Tech (Electronics & Computer Science)

🤖 Aspiring AI/ML Engineer

💡 **Interests:** Machine Learning • NLP • Deep Learning • LLMs • Causal AI

---

⭐ **If you found this project useful, consider giving it a star!**
