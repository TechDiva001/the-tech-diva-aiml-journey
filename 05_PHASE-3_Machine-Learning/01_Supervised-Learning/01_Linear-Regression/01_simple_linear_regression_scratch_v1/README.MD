# Linear Regression from Scratch

**Simple linear regression built by hand in plain Python and NumPy. No classes, no objects, and no scikit-learn anywhere in the model.**

Predicting salary from years of experience, with every formula written, tested and explained step by step.

Built by **Benedicta Bondzie, The Tech Diva** | [LinkedIn](https://www.linkedin.com/in/benedicta-bondzie-the-tech-diva/)

---

## Table of contents

1. [Overview](#overview)
2. [Why I built this](#why-i-built-this)
3. [What "from scratch" means here](#what-from-scratch-means-here)
4. [The dataset](#the-dataset)
5. [Repository contents](#repository-contents)
6. [How the notebook is organised](#how-the-notebook-is-organised)
7. [The maths](#the-maths)
8. [Results](#results)
9. [Verified against scikit-learn](#verified-against-scikit-learn)
10. [Assumption checks](#assumption-checks)
11. [A lesson about missing values](#a-lesson-about-missing-values)
12. [Limitations](#limitations)
13. [What I would do next](#what-i-would-do-next)
14. [How to run it](#how-to-run-it)
15. [Acknowledgements](#acknowledgements)

---

## Overview

This project answers one question: **can a straight line predict a person's salary from their years of experience, and can I build that line myself using only basic maths?**

The notebook walks through the whole process from a messy CSV to a finished, tested and explained model:

- load and inspect the data
- clean the missing values
- split the data into training and testing sets by hand
- calculate the slope and the intercept with the sum formulas
- make predictions
- evaluate the model with five metrics, all written as my own functions
- visualise the regression line
- check the assumptions that linear regression depends on
- verify the result against scikit-learn
- explain what was found, in plain words

It is written so that a beginner can read it from top to bottom, understand the maths behind linear regression, and then rebuild it themselves. Every step has a markdown explanation, and every function says what it takes in, what it returns and why it exists.

## Why I built this

I wanted to know what a machine learning library does underneath, instead of only calling `.fit()` and `.predict()`. If I can write the slope formula, the predictions and the metrics myself, then when I use a library later I understand what it is doing for me.

I have not learned classes and objects yet, so this project uses **plain functions only**. When I learn classes, I plan to rebuild it with them.

## What "from scratch" means here

| Tool | What it was allowed to do |
|---|---|
| **NumPy** | All of the maths: sums, means, slope, intercept, predictions and metrics |
| **pandas** | Load the CSV, inspect it and clean it. Nothing else |
| **matplotlib and seaborn** | Draw charts only. They never calculate anything for the model |
| **scikit-learn** | Not used in the model. It appears **once, in the last cell**, only to check my answer |
| **Classes and objects** | Not used. Everything is plain functions |

I wrote nine functions by hand: `fit`, `predict`, `mse`, `mae`, `rmse`, `r2`, `adjusted_r2`, `residuals` and `correlation`.

## The dataset

The dataset is **synthetic**. I generated it to look like a salary dataset, with salary rising as years of experience rises, plus natural scatter. It is not real salary data, so the results show that the method works and say nothing about real salaries anywhere.

| Column | Meaning |
|---|---|
| `YearsExperience` | Years of experience (a decimal, for example 7.5 is seven and a half years) |
| `Salary` | Salary |

Two versions of the same data are included:

- **`Salary_Data_100_messy.csv`** has 100 rows with **12 missing values** (6 in each column), placed on purpose so that cleaning the data is part of the project. This is the file the model is built on.
- **`Salary_Data_100_clean.csv`** is the same data with nothing missing. It is used **only to check that my `fit` function is correct**, and it is not used to train the model.

## Repository contents

```
.
|-- README.md
|-- Linear_Regression_From_Scratch.ipynb    the full notebook
|-- Salary_Data_100_messy.csv               data with missing values (used for the model)
|-- Salary_Data_100_clean.csv               complete copy (used only to check my functions)
|-- requirements.txt                        libraries needed to run the notebook
```

## How the notebook is organised

1. **Setup**: import the libraries.
2. **Load the data**: read the messy CSV.
3. **Inspect the data**: data types, summary statistics, missing values.
4. **Clean the data**: drop the rows with missing values (100 rows become 88).
5. **Move to NumPy**: turn the columns into arrays and plot the cleaned data.
6. **Split by hand**: 70 rows for training and 18 for testing, using slicing.
7. **Check the ranges**: confirm the test data sits inside the range of the training data.
8. **Write the functions**: the nine functions, each with an explanation.
9. **Check the functions**: test them on answers I already know.
10. **Train**: find the slope and the intercept from the training data only.
11. **Predict**: on both the training and the testing data.
12. **Visualise**: the regression line against the training data, the testing data, and both together.
13. **Evaluate**: all five metrics on both sets, side by side.
14. **Residuals**: the error for every row.
15. **Assumptions**: linearity, independence, normality, constant variance and multicollinearity.
16. **The story**: what I found, what to be careful about, and the questions I asked while building it.
17. **What I would do next.**
18. **Final check**: compare with scikit-learn.

## The maths

For n rows, with x as years of experience and y as salary:

**Slope**

m = (n × Σxy − Σx × Σy) / (n × Σx² − (Σx)²)

**Intercept**

b = (Σy − m × Σx) / n

**Prediction**

ŷ = mx + b

**Evaluation metrics**

MSE = (1/n) × Σ(yᵢ − ŷᵢ)²

MAE = (1/n) × Σ|yᵢ − ŷᵢ|

RMSE = √MSE

R² = 1 − [Σ(yᵢ − ŷᵢ)² / Σ(yᵢ − ȳ)²]

R²_adj = 1 − (1 − R²) × (n − 1) / (n − k − 1)

Here k is the number of features, which is 1 in this project.

Two things that are easy to mix up in the slope formula: Σx² means square each value first and then add them up, while (Σx)² means add them up first and then square the total.

I also explained how to calculate the slope and the intercept by hand in a LinkedIn post: **[read it here](https://lnkd.in/p/dpdJfcjg)**.

## Results

The model learned from the 70 training rows is:

> **Salary is about 27,672 + 9,118 x years of experience**

Each extra year of experience goes with about 9,118 more in salary, and a person with zero years is predicted to earn about 27,672.

| Metric | Training (70 rows) | Testing (18 rows) |
|---|---|---|
| MSE | about 47,572,718 | about 85,431,911 |
| MAE | about 5,797 | about 7,671 |
| RMSE | about 6,897 | about 9,243 |
| R-squared | 0.965 | 0.922 |
| Adjusted R-squared | 0.965 | 0.917 |

**How to read this:** the model explains about 96.5% of the variation in salary on the data it learned from and about 92.2% on people it had never seen. The test RMSE of about 9,243 is roughly 9% of the average salary. The gap between training and testing is small, which suggests the model learned a real pattern instead of memorising rows. The test set has only 18 rows, so one unusual person can move the test score noticeably.

## Verified against scikit-learn

As a last proof, the final cell of the notebook runs scikit-learn's `LinearRegression` on the **same training and testing rows** and compares it with my own results. The library is used only to check my work and never produced any of my results.

| | Mine | scikit-learn |
|---|---|---|
| Slope | 9117.665059179164 | 9117.665059179151 |
| Intercept | 27672.46409098011 | 27672.46409098021 |

The slope and intercept agree to about 10 decimal places, and the first five test predictions are identical. The tiny differences far out in the decimals are computer rounding.

## Assumption checks

Linear regression gives trustworthy results only if some conditions hold. I checked each one with a chart.

| Assumption | Result |
|---|---|
| **Linearity** | Holds. The correlation is about 0.98 and the scatter plot is a straight band |
| **Independence of errors** | No pattern seen, but not fully testable, because the rows have no time order |
| **Normality of errors** | Roughly holds. The histogram is not a perfect bell, but there is no serious problem |
| **Constant variance** | Holds. The residuals form an even band with no funnel shape |
| **No multicollinearity** | Not applicable, because there is only one feature |

The checks pass partly because the data is synthetic and was generated from a straight line plus random noise. Real data is messier, and the same checks might show problems.

## A lesson about missing values

My first attempt filled the missing values with the column mean, because it is quick and many people do it. The model looked fine on the training set and noticeably worse on the testing set:

| Missing values handled by | Training R-squared | Testing R-squared | Testing RMSE |
|---|---|---|---|
| Filling with the mean (earlier run) | 0.905 | 0.774 | about 16,000 |
| **Dropping the incomplete rows (final)** | **0.965** | **0.922** | **about 9,243** |

I first suspected the train and test split, and then the range of the test data. Neither was the cause. When I looked at the **largest test error**, it belonged to a row where the experience had been invented by the mean fill. That one made-up row caused more than half of the whole test error. A filled-in value creates a data point that never existed, and in a regression it can sit far from the real line.

**What I took from it:** do not pick a way to handle missing values just because it is the default. Try the options (drop, fill with the mean, fill with the median), keep the test set the same, and let the evaluation metrics decide. Whenever a score looks wrong, look at where the biggest errors come from.

The mean-fill run is not in the notebook's code, because I replaced it with the final version. It is described in Step 4 of the notebook.

## Limitations

- The data is **synthetic**, so the results are not facts about real salaries.
- The model shows an **association**, not a cause.
- The line is only reliable **inside the range of the data**, about 0.5 to 14.5 years of experience.
- The testing set is small (18 rows), so the test scores are a good guide and not an exact measure.
- 12 rows were dropped during cleaning.
- I cleaned the data before splitting it. The stricter approach is to split first, to avoid data leakage.

## What I would do next

- Split the data **before** cleaning, to avoid data leakage.
- Use a bigger dataset and test more than once (k-fold cross-validation).
- Compare ways of handling missing values properly, in one table.
- Build the same model with **gradient descent** and compare it with the formula answer.
- Extend it to **multiple linear regression** with matrix maths.
- Learn **regularisation** (Ridge, Lasso and Elastic Net).
- Wrap the functions in a **class** once I have learned classes and objects.
- Apply the same method to a **real problem from Ghana or Africa** with real data.

## How to run it

**In Google Colab (easiest):**

1. Open [colab.research.google.com](https://colab.research.google.com) and upload `Linear_Regression_From_Scratch.ipynb`.
2. Upload `Salary_Data_100_messy.csv` and `Salary_Data_100_clean.csv` using the Files panel on the left.
3. Run the cells from top to bottom.

**On your own computer:**

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
pip install -r requirements.txt
jupyter notebook Linear_Regression_From_Scratch.ipynb
```

Keep the two CSV files in the same folder as the notebook, and run the cells from top to bottom.

## Acknowledgements

Thank you to **GeeksforGeeks** for the learning material that gave me the foundation for this project.

---

*Built by Benedicta Bondzie, The Tech Diva.*

*If you get stuck anywhere in the code, the notebook explains each step in plain words, and my LinkedIn post on calculating the slope by hand goes through the formula slowly. Find me on [LinkedIn](https://www.linkedin.com/in/benedicta-bondzie-the-tech-diva/).*
