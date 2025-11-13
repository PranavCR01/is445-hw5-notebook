---
layout: default
title: "IS445 HW5 – Two Altair/Vega-Lite Visualizations"
---

# IS445 Homework 5  
### Pranav Charakondala – Data Visualizations Using Altair & Vega-Lite  

---

# Links  
- **Link to Data:**  
  https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/building_inventory.csv  

- **Link to Python Notebook:**  
  [hw5.ipynb](hw5.ipynb)

---

# Plot 1: Building Square Footage vs Year Constructed

<iframe src="chart1.html" width="100%" height="600px"></iframe>

## What this plot visualizes  
This scatter plot shows the relationship between **year constructed** and **square footage** for buildings in the Illinois Building Inventory dataset.  
It helps identify trends such as whether newer buildings tend to be larger or smaller.

## Design Choices (Encodings)
- **X-axis:** `year_constructed` (quantitative)  
- **Y-axis:** `square_footage` (quantitative)  
- **Color:** `city` (nominal)  
  - A color legend helps identify clusters by location.
- **Size:** Kept constant to avoid misleading emphasis.

## Colormap Choices
- Vega-Lite’s default categorical palette works well because:
  - The variable (`city`) has many categories.
  - A qualitative palette avoids implying numeric ordering.

## Data Transformations
- Converted arrays into lists using  
  `df[col_name].apply(to_list_if_array)`  
- Removed rows with missing year or square footage.  
- Ensured numerical columns were cast to ints/floats.

These transformations ensured Altair could correctly encode the data.

## Interactivity  
This visualization includes **pan and zoom interaction**, making it easier to examine specific ranges of years and outlier buildings.  
Interactivity helps when exploring dense scatter plots with many overlapping points.

---

# Plot 2: Number of Buildings per City

<iframe src="chart2.html" width="100%" height="600px"></iframe>

## What this plot visualizes  
This bar chart displays the **count of buildings** for each Illinois city appearing in the dataset.  
It highlights which cities have the largest building counts (e.g., Springfield, Carbondale).

## Design Choices (Encodings)
- **X-axis:** `city` (nominal)  
- **Y-axis:** building count (quantitative)  
- **Sorting:** Cities are sorted in descending frequency to make comparisons clearer.
- **Color:** Single neutral color to avoid implying additional variables.

## Colormap Choices
A single color was intentionally chosen to:
- Emphasize counts rather than categories  
- Prevent visual overload (many city names)

## Data Transformations
- Grouped data using Pandas:  
  ```python
  df.groupby("city").size().reset_index(name="count")
