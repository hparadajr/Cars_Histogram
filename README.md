# mtcars Plotting Script

## What the script does
- Loads required packages (`ggplot2`, `dplyr`).
- Prepares the `mtcars` dataset:
  - Adds a `car` column with row names.
  - Converts `cyl` to a factor.
- Creates an output directory `plots/` (if it doesn't exist).
- Generates and saves three plots:
  1. Scatterplot of Horsepower vs MPG with a linear fit 
  2. Histogram of MPG
  3. Boxplot of MPG by cylinder count 
- Prints MPG summary statistics (average, min, max) grouped by cylinder to the console.

---

## Expected console output
When you run the script you will see a message and a summary table similar to:

```text
=== MPG SUMMARY BY CYLINDER COUNT ===
  cyl   Avg_MPG Min_MPG Max_MPG
  <fct>   <dbl>   <dbl>   <dbl>
1 4       26.7      21    33.9
2 6       19.7      17    21.4
3 8       15.1      10    19.2
```

---

## Requirements
- R packages:
  - ggplot2
  - dplyr

```r
install.packages(c("ggplot2", "dplyr"))

---

## Usage
The script will:
- Create `plots/` if it does not exist.
- Print each plot to the active graphics device 
- Save PNG files in `plots/`.
- Print the MPG summary to the console.

---
