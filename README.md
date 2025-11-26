# mtcars Plotting Script

## Dataset
- Built-in R dataset: `mtcars`
- Contains fuel consumption and 10 aspects of automobile design and performance for 32 automobiles between the years 1973–1974
- Columns used in the script:
  - mpg — Miles/(US) gallon
  - hp — Gross horsepower
  - cyl — Number of cylinders (converted to a factor in the script)
  - row names are added as a `car` column for reference
    
## Skills demonstrated
- R scripting and reproducible workflows
- Data wrangling with dplyr
- Data visualization with ggplot2 (scatterplot, histogram, boxplot)
- Creating output directories and saving plot artifacts (ggsave)
- Basic use of package installation
- Generating summary statistics
  
## What the script does
- Loads required packages (`ggplot2`, `dplyr`).
- Prepares the `mtcars` dataset:
  - Adds a `car` column from the row names.
  - Converts `cyl` to a factor for categorical plotting.
- Ensures an output directory `plots/'
- Produces three visualizations using ggplot2:
  1. Scatterplot of Horsepower vs MPG with a linear fit 
  2. Histogram of MPG (binwidth = 3, fill = green)
  3. Boxplot of MPG by cylinder count
- Calculates and prints summary statistics (average, min, max MPG) grouped by cylinder.

## Example R script
```r
# r2.R
# Generates three ggplot2 plots from the mtcars dataset and prints MPG summary by cylinder.

required_packages <- c("ggplot2", "dplyr")

install_if_missing <- function(pkgs) {
  for (p in pkgs) {
    if (!suppressWarnings(require(p, character.only = TRUE))) {
      message(sprintf("Package '%s' is not installed. Installing now...", p))
      install.packages(p, repos = "https://cloud.r-project.org")
      library(p, character.only = TRUE)
    }
  }
}

install_if_missing(required_packages)

library(ggplot2)
library(dplyr)

# Data prep
data <- mtcars
data$car <- rownames(mtcars)
data$cyl <- as.factor(data$cyl)

# Create output directory for plots
out_dir <- "plots"
if (!dir.exists(out_dir)) dir.create(out_dir, showWarnings = FALSE)

# 1 — Scatterplot: Horsepower vs MPG
plot_hp_mpg <- ggplot(data, aes(x = hp, y = mpg)) +
  geom_point(size = 3) +
  geom_smooth(method = "lm", se = FALSE, color = "blue") +
  labs(
    title = "Horsepower vs MPG",
    x = "Horsepower",
    y = "Miles Per Gallon"
  ) +
  theme_minimal()

print(plot_hp_mpg)
ggsave(filename = file.path(out_dir, "hp_vs_mpg.png"), plot = plot_hp_mpg, width = 7, height = 5, dpi = 300)

# 2 — Histogram of MPG
plot_hist_mpg <- ggplot(data, aes(x = mpg)) +
  geom_histogram(binwidth = 3, fill = "green") +
  labs(
    title = "Distribution of Miles Per Gallon",
    x = "MPG",
    y = "Count"
  ) +
  theme_minimal()

print(plot_hist_mpg)
ggsave(filename = file.path(out_dir, "mpg_histogram.png"), plot = plot_hist_mpg, width = 7, height = 5, dpi = 300)

# 3 — Boxplot of MPG by number of cylinders
plot_box_cyl <- ggplot(data, aes(x = cyl, y = mpg, fill = cyl)) +
  geom_boxplot() +
  labs(
    title = "MPG by Cylinder Count",
    x = "Cylinders",
    y = "MPG"
  ) +
  theme_minimal() +
  scale_fill_brewer(palette = "Set2")

print(plot_box_cyl)
ggsave(filename = file.path(out_dir, "mpg_by_cyl_boxplot.png"), plot = plot_box_cyl, width = 7, height = 5, dpi = 300)

# --- Summary statistics ---
mpg_summary <- data %>%
  group_by(cyl) %>%
  summarize(
    Avg_MPG = mean(mpg),
    Min_MPG = min(mpg),
    Max_MPG = max(mpg),
    .groups = "drop"
  )

message("=== MPG SUMMARY BY CYLINDER COUNT ===")
print(mpg_summary)
```

## Results (from the above run)
The run produced three PNG files (saved to `plots/`) and printed the MPG summary by cylinder. Below are the relevant results.

Saved plot files:
- plots/hp_vs_mpg.png      (Image 1)
- plots/mpg_histogram.png  (Image 2)
- plots/mpg_by_cyl_boxplot.png (Image 3)

Embedded outputs (if the images are present in `plots/`, they will render inline on GitHub):

Image 1 — Horsepower vs MPG (scatterplot with linear fit)

<img src="plots/hp_vs_mpg.png" alt="Image 1 — Horsepower vs MPG" style="max-width:100%;height:auto;" />

Image 2 — Distribution of Miles Per Gallon (histogram)

<img src="plots/mpg_histogram.png" alt="Image 2 — Distribution of Miles Per Gallon" style="max-width:100%;height:auto;" />

Image 3 — MPG by Cylinder Count (boxplots)

<img src="plots/mpg_by_cyl_boxplot.png" alt="Image 3 — MPG by Cylinder Count" style="max-width:100%;height:auto;" />

Console summary (exact text printed during the run):

```
=== MPG SUMMARY BY CYLINDER COUNT ===
# A tibble: 3 × 4
  cyl   Avg_MPG Min_MPG Max_MPG
  <fct>   <dbl>   <dbl>   <dbl>
1 4       26.7      21    33.9
2 6       19.7      17    21.4
3 8       15.1      10    19.2
```

