# ANOVA and Linear Regression Toolbox

A comprehensive Python toolbox for statistical analysis implementing one-way ANOVA, two-way ANOVA, and multiple linear regression with various hypothesis testing and confidence interval methods.

## Features

- **One-Way ANOVA**: Group comparison, contrast analysis, multiple comparison corrections
- **Two-Way ANOVA**: Two-factor analysis with interaction effects
- **Multiple Linear Regression**: Parameter estimation, hypothesis testing, prediction intervals
- **Statistical Methods**: Bonferroni, Sidak, Scheffe, and Tukey corrections
- **Confidence Intervals**: Individual and simultaneous confidence intervals

## Requirements

```python
numpy
scipy
```

## Installation

Clone this repository:
```bash
git clone https://github.com/MekanMyradov/anova-linear-regression-stats-toolbox.git
cd anova-linear-regression-stats-toolbox
```

Install dependencies:
```bash
pip install numpy scipy
```

## API Reference

### One-Way ANOVA Functions

#### `anova1_partition_tss(X)`
Partitions total sum of squares into between-group and within-group components.

**Parameters:**
- `X`: 2D array where rows are groups, columns are observations

**Returns:**
- `ss_total`: Total sum of squares
- `ss_w`: Within-group sum of squares  
- `ss_b`: Between-group sum of squares

#### `anova1_test_equality(X, alpha=0.05)`
Tests equality of group means and prints ANOVA table.

**Parameters:**
- `X`: 2D array of group data
- `alpha`: Significance level (default: 0.05)

**Returns:**
Dictionary with F-statistic, p-value, critical value, sum of squares, degrees of freedom, mean squares, and decision.

#### `anova1_ci_linear_combs(X, alpha, C, method="best")`
Computes simultaneous confidence intervals for linear combinations of group means.

**Parameters:**
- `X`: List of arrays, each containing observations for one group
- `alpha`: Significance level
- `C`: Matrix where each row defines a linear combination
- `method`: "Scheffe", "Tukey", "Bonferroni", "Sidak", or "best"

**Returns:**
- List of confidence interval tuples
- Method used

### Two-Way ANOVA Functions

#### `anova2_partition_tss(X)`
Partitions total sum of squares for two-factor analysis.

**Parameters:**
- `X`: 3D array where X[i,j,k] is the k-th observation in cell (i,j)

**Returns:**
- `ss_total`: Total sum of squares
- `ss_a`: Factor A sum of squares
- `ss_b`: Factor B sum of squares
- `ss_ab`: Interaction sum of squares
- `ss_e`: Error sum of squares

#### `anova2_test_equality(X, alpha=0.05, test_type="A")`
Tests main effects or interaction in two-way ANOVA.

**Parameters:**
- `X`: 3D array of data
- `alpha`: Significance level
- `test_type`: "A" (factor A), "B" (factor B), or "AB" (interaction)

### Linear Regression Functions

#### `mult_lr_least_squares(X, y)`
Computes least squares estimates for regression coefficients.

**Parameters:**
- `X`: n×(k+1) design matrix with first column of ones
- `y`: n×1 response vector

**Returns:**
- `beta_hat`: Estimated regression coefficients
- `sigma2_hat`: MLE of error variance
- `sigma2_hat_unbiased`: Unbiased estimate of error variance

#### `mult_norm_lr_simul_ci(X, y, alpha=0.05)`
Computes simultaneous confidence intervals for regression coefficients.

#### `mult_norm_lr_test_general(X, y, C, c0, alpha=0.05)`
Tests general linear hypothesis H₀: Cβ = c₀.

#### `mult_norm_lr_pred_ci(X, y, D, alpha=0.05, method="best")`
Computes prediction confidence intervals.

### Utility Functions

#### `bonferroni_correction(alpha, m)`
Computes individual test significance level using Bonferroni correction.

#### `sidak_correction(alpha, m)`
Computes individual test significance level using Sidak correction.

#### `anova1_is_contrast(c)`
Checks if linear combination coefficients form a contrast (sum = 0).

#### `anova1_is_orthogonal(group_sizes, coef1, coef2)`
Checks if two contrasts are orthogonal.

## Examples

### One-Way ANOVA Example Output
```
ANOVA Table
-----------------------------------------------------------
Source    df    SS        MS        F
-----------------------------------------------------------
Between   2     106.5830  53.2915   15.2559
Within    42    146.7128  3.4932
Total     44    253.2957
-----------------------------------------------------------
Critical value: 3.2199
p-value: 0.00001046
Decision: Reject H0
```

### Linear Regression Example Output
```
True beta: [2.0, 1.5, -0.5, 0.8]
Estimated beta: [2.0769, 1.6040, -0.4652, 0.9647]
95.0% CI for beta_0: (1.8249, 2.3289)
95.0% CI for beta_1: (1.3922, 1.8157)
```

## Methods Implemented

- **Multiple Comparison Corrections**: Bonferroni, Sidak, Scheffe, Tukey
- **Hypothesis Testing**: F-tests for ANOVA, general linear hypothesis tests
- **Confidence Intervals**: Individual and simultaneous intervals
- **Parameter Estimation**: Maximum likelihood and least squares estimation
