# Netflix Analysis Project

## Overview

This project analyzes the Netflix titles dataset to explore patterns in movies and TV shows, including content type distribution and release trends. 

What started as a simple exploratory notebook gradually developed into a more structured and reproducible data analysis project. Over time, I focused not just on producing visualizations, but on improving organization, cleaning logic, and version control practices.


## How the Project Evolved

### Toddler Branch (Early Version)

In the early stage of this project, I focused mainly on exploratory data analysis. I created visualizations, experimented with cleaning steps, and exported HTML and Markdown versions of the notebook.

However, this version had several issues:

- File paths were machine-specific.
- The notebook did not reliably run from the first cell.
- Cleaning logic was not fully stable.
- Some decisions were experimental rather than structured.

I kept this branch in the repository to show how the project developed over time.

---

### Final Version

In the final version, I made significant improvements to strengthen the project:

- Reorganized the folder structure for clarity.
- Cleaned up the `.gitignore` file to properly manage data tracking.
- Replaced hard-coded paths with relative paths to improve portability.
- Ensured the notebook runs from start to finish without manual fixes.
- Identified and fixed a datetime parsing issue that was accidentally removing all rows during cleaning.
- Stabilized the data cleaning process to prevent unintended data loss.
- Improved commit messages to better reflect development decisions.

These changes made the project more reproducible, structured, and maintainable.

---

## Dataset

The project uses the public Netflix titles dataset, which includes:

- Content type (Movie or TV Show)
- Title
- Director
- Cast
- Country
- Date added
- Release year
- Rating
- Duration
- Genres
- Description

---

## Analysis Process

The workflow follows these steps:

1. Load the dataset.
2. Clean and handle missing values.
3. Convert and standardize date fields.
4. Prepare features for analysis.
5. Perform exploratory analysis.
6. Generate visualizations comparing Movies and TV Shows.
7. Export a cleaned dataset for reproducibility.

---

## Reproducibility

The final notebook is designed to:

- Run from the first cell without errors.
- Avoid hard-coded file paths.
- Use relative paths for loading and saving data.
- Maintain clean and meaningful version control history.

---

## Conclusion

This project reflects my growth in data cleaning, debugging, and version control. 

The final version represents a shift from exploratory experimentation toward a more structured and professional data analysis workflow.