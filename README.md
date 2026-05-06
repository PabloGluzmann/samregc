# samregc

**samregc** is a Stata package for robust and systematic sensitivity analysis of regression coefficients. It performs all-subset regression analyses to assess how coefficient estimates change as different combinations of covariates are included or excluded from the model. This approach allows researchers to transparently evaluate the robustness of their findings.

## Features

- Systematic sensitivity/robustness analysis for selected regression coefficients.
- Executes all-subset regressions based on combinations of user-specified covariate sets.
- Flexible specification: supports single variables, groups, and forced-in variables.
- Compatible with a range of regression commands (`regress` by default; also `xtreg`, `ivregress`, etc.).
- Outputs comprehensive results including all regression coefficients, t-statistics, and model dimensions.
- Generates Excel tables and kernel density plots summarizing distribution of coefficients and significance across all regressions.
- Options for fixed covariates, minimum/maximum combination size, sample handling, and automating output file names and formats.

## Installation

To install `samregc` in Stata, use:

```
ssc install samregc
```

Or download the `.ado` and `.sthlp` files and copy them to your Stata `PLUS` directory.

## Basic Usage

Run a sensitivity analysis on the coefficient for `main`, iterating over `svar1` and `svar2`:

```
. samregc depvar main, iterateover(svar1 svar2)
```

This will automatically run all combinations of the main variable plus each subset of the iteration variables, saving results to `samregc.dta` (Stata data) and summary tables/plots to `samregc.xlsx` and `.gph` files.

### Example

```stata
. sysuse auto
. samregc price mpg, iterateover(weight length)
```

This will examine how the coefficient of `mpg` in predicting car price changes as `weight`, `length`, or both are included/excluded from the model.

## Syntax Summary

```
samregc depvar Main_Varlist [if] [in] [weight], iterateover(Iteration_Varlist) [options]
```

- `iterateover()`: Specifies variables whose covariate subsets will be iterated over.
- `griterateover()`: Iterate over groups of covariates.
- `fixvar()`: Force variables to appear in every regression.
- `ncomb(min,max)`: Restrict subset size to between min and max.
- `cmdest()`: Use an alternative estimation command (e.g., `xtreg`, `ivregress`).
- `resultsdta()`, `replace`, `double`, `nograph`, `noexcel`, `graphtype()`, etc.: Flexible output options.

See the `.sthlp` file or sample below for the full option set and advanced usage.

## Output

- **samregc.dta**: Dataset with regression results for each submodel. Columns include:
  - `order`: Regression ID
  - `v_1_b`, `v_2_b`, ...: Coefficients for main and iteration variables
  - `v_1_t`, `v_2_t`, ...: Associated t-statistics
  - `obs`: Number of observations
  - `nvar`: Number of covariates
  - `rank`: Rank of model matrix (accounts for collinearity)
  - `omitted`: Indicator for dropped variables

- **samregc.xlsx**: Excel summary of coefficient robustness and share/significance across models.

- **Graph files** (`.gph`, `.png`, etc): Kernel density plots and more for coefficients and t-stats.

## Why Use samregc?

Transparency regarding robustness to covariate choice is a core aspect of empirical credibility. By automating all-subset regressions, `samregc`:
- Frees researchers from tedious manual model variations.
- Provides a complete landscape of how key results change with co-variate specification.
- Facilitates very clear visual and tabular reporting for publications.

## Authors

- Pablo Gluzmann (CEDLAS-FCE-UNLP, CONICET, La Plata, Argentina)  
  gluzmann@gmail.com  
- Demian Panigo (Instituto Malvinas, UNLP, CONICET, La Plata, Argentina)  
  panigo@gmail.com

## License

MIT License. See [LICENSE](LICENSE) for details.

## Further Reading

- Stata help file: [samregc.sthlp](samregc.sthlp)
- Related Stata commands: `checkrob`, `multivrs`

---

*Please cite the authors if you use `samregc` in published work.*

=====================================
