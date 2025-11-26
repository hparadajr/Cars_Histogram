# mtcars Plotting Script

This repository contains an R script (originally provided as `r2.txt`) that generates three plots and summary statistics from the built-in `mtcars` dataset and saves the plots to a `plots/` folder.

This README embeds the generated images directly so you can see them inline instead of just seeing links. For the images to render here on GitHub, make sure the PNG files are committed to the `plots/` directory at the repository root:
- plots/hp_vs_mpg.png
- plots/mpg_histogram.png
- plots/mpg_by_cyl_boxplot.png

If those files exist in the `plots/` directory, the images below will be displayed directly in this README.

---

## What the script does
- Loads required packages (`ggplot2`, `dplyr`).
- Prepares the `mtcars` dataset:
  - Adds a `car` column with row names.
  - Converts `cyl` to a factor.
- Creates an output directory `plots/` (if it doesn't exist).
- Generates and saves three plots:
  1. Scatterplot of Horsepower vs MPG with a linear fit → `plots/hp_vs_mpg.png`
  2. Histogram of MPG (binwidth = 3, fill = green) → `plots/mpg_histogram.png`
  3. Boxplot of MPG by cylinder count → `plots/mpg_by_cyl_boxplot.png`
- Prints MPG summary statistics (average, min, max) grouped by cylinder to the console.

---

## Output images (embedded)

Image 1 — Horsepower vs MPG (scatterplot with linear fit)

<img src="plots/hp_vs_mpg.png" alt="Image 1 — Horsepower vs MPG" style="max-width:100%;height:auto;" />

Image 2 — Distribution of Miles Per Gallon (histogram)

<img src="plots/mpg_histogram.png" alt="Image 2 — Distribution of Miles Per Gallon" style="max-width:100%;height:auto;" />

Image 3 — MPG by Cylinder Count (boxplots)

<img src="plots/mpg_by_cyl_boxplot.png" alt="Image 3 — MPG by Cylinder Count" style="max-width:100%;height:auto;" />

Mapping of image numbers to files:
- Image 1: plots/hp_vs_mpg.png
- Image 2: plots/mpg_histogram.png
- Image 3: plots/mpg_by_cyl_boxplot.png

---

## Expected console output
When you run the script you will see a message and a summary table similar to:

```text
=== MPG SUMMARY BY CYLINDER COUNT ===
# A tibble: 3 × 4
  cyl   Avg_MPG Min_MPG Max_MPG
  <fct>   <dbl>   <dbl>   <dbl>
1 4       26.7      21    33.9
2 6       19.7      17    21.4
3 8       15.1      10    19.2
```

---

## Requirements
- R (version 3.5+ recommended)
- R packages:
  - ggplot2
  - dplyr
- Optional (for brewer palettes used in the boxplot): `RColorBrewer`

Install required packages in R if they are missing:

```r
install.packages(c("ggplot2", "dplyr"))
# If you encounter palette errors:
install.packages("RColorBrewer")
```

---

## Usage
1. Ensure the script file (rename `r2.txt` to `r2.R` if desired) is in the repository root.
2. Run from terminal:
```bash
Rscript r2.R
```
Or run interactively in RStudio by sourcing the file.

The script will:
- Create `plots/` if it does not exist.
- Print each plot to the active graphics device (useful for interactive sessions).
- Save PNG files in `plots/`.
- Print the MPG summary to the console.

---

## Notes on inline images
- The README uses standard HTML `<img>` tags pointing to the relative file paths in `plots/`. GitHub renders these images inline when the files are present in the repo at those paths.
- If you want the README to show images even before committing PNG files, you can embed images using base64 data URIs, but that is not recommended because it makes the README very large and hard to edit. The approach used here is the most common and Git-friendly: commit the image files into the repo and reference them with relative paths.
- If the images do not display after committing, confirm the files are in the `plots/` folder at the repository root and that their names exactly match those referenced above.

---

## Customization
- Change plot appearance (colors, themes) by editing the ggplot code in the script.
- Adjust `ggsave()` parameters (width, height, dpi) or change file extensions to save PDF/SVG.
- Change the histogram `binwidth` to modify bin sizing.

---

## Troubleshooting
- If `ggplot2` or `dplyr` fail to load, run `install.packages()` as shown above.
- If `scale_fill_brewer()` produces an error, ensure `RColorBrewer` is installed.

---

## Next steps (optional)
- Convert the script to an RMarkdown report (`.Rmd`) to combine the plots and summary into a single HTML or PDF report.
- Add additional exploratory plots or regression diagnostics.
- Add a small CI workflow to run the script automatically (e.g., GitHub Actions that runs Rscript).

License
- Add a license of your choice, or let me know if you want a recommended license file added.
