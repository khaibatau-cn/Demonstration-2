# Plugged In - COS30045 Exercises 4 to 6

COS30045 Data Visualisation, Swinburne University

**Plugged In** is a small website that brings together my D3.js exercises from Weeks 4 to 6. Each exercise has its own page, and a shared navigation bar links them together. Most of the charts use Australian TV energy data from the Energy Rating register.

---

## Contents

1. [Pages](#pages)
2. [Folder structure](#folder-structure)
3. [Exercise 4.1 - SVG house](#exercise-41---svg-house)
4. [Exercises 4.3 to 4.6 - Bar chart](#exercises-43-to-46---bar-chart)
5. [Exercise 5 - Multi-chart page](#exercise-5---multi-chart-page)
6. [Exercise 6 - Interactivity](#exercise-6---interactivity)
7. [Data](#data)
8. [How to run locally](#how-to-run-locally)
9. [GitHub repositories](#github-repositories)
10. [Technologies](#technologies)
11. [GenAI use](#genai-use)

---

## Pages

| Page | Folder | What it shows |
|---|---|---|
| Home | `index.html` | Links to all four exercises |
| Exercise 4.1 | `4.1/` | A house scene drawn with SVG shapes |
| Exercises 4.3 to 4.6 | `4.x/` | Horizontal bar chart of TV models by brand |
| Exercise 5 | `5.x/` | Bar chart, line chart and donut chart on one page |
| Exercise 6 | `6.x/` | Histogram with filters and scatterplot with tooltips |

Every page has the same layout: navigation bar, header with key numbers, one card per chart, and a footer. Clicking **Plugged In** in the navigation bar returns to the home page.

---

## Folder structure

```
Exercises/
├── index.html                  home page
├── css/site.css                shared page styles
│
├── 4.1/                        Exercise 4.1 - SVG house
│   ├── index.html
│   ├── css/site.css
│   └── images/                 annotated drawing and DevTools screenshot
│
├── 4.x/                        Exercises 4.3 to 4.6 - bar chart
│   ├── index.html
│   ├── main.js
│   ├── css/site.css, css/style.css
│   └── data/ex.csv
│
├── 5.x/                        Exercise 5 - multi-chart page
│   ├── index.html
│   ├── css/site.css, css/style.css
│   ├── js/barChart.js, js/line-chart.js, js/donut-chart.js
│   └── data/                   tv55ScreenTech.csv, ARE_Spot_Prices.csv, tv_size_count.csv,
│                               tv_2026_02_15.csv
│
└── 6.x/                        Exercise 6 - interactivity
    ├── index.html
    ├── css/site.css, css/base.css, css/visualization.css
    ├── js/load-data.js, js/shared-constants.js, js/interactions.js,
    │   js/histogram.js, js/scatterplot.js
    ├── data/Ex6_TVdata_withStar.csv
    └── W6 TV Data.knwf
```

Each exercise folder has its own copy of `css/site.css`, so every folder works on its own as a separate GitHub repository.

---

## Exercise 4.1 - SVG house

A house scene drawn on a 400 x 400 SVG canvas.

- **Shapes:** `rect` (sky, walls, door, fence), `circle` (sun, clouds, leaves, flowers), `ellipse` (hills), `polygon` (roof) and `path` (garden path)
- **Coordinates:** (0, 0) is the top-left corner; x grows to the right and y grows downwards
- **Data joins:** fence posts, clouds, smoke, windows, trunks, leaves and flowers are created from arrays with `.data().join()`
- **Drawing order:** shapes drawn later sit on top, so the sky is drawn first and the chimney before the roof

The page also includes an annotated version of the drawing and a screenshot of the SVG in the browser DevTools (F12 > Elements).

---

## Exercises 4.3 to 4.6 - Bar chart

A horizontal bar chart of the number of TV models per brand.

- SVG canvas with a `viewBox` so the chart scales with the page
- Data loaded with `d3.csv()`, counts converted to numbers and sorted from most to fewest
- `d3.scaleLinear()` for bar length and `d3.scaleBand()` for spacing the brands
- One group (`g`) per brand holding the bar, brand name and count

**Result:** Samsung has the most models (1,096), followed by Kogan (788) and LG (677).

---

## Exercise 5 - Multi-chart page

Three charts on one page, one JavaScript file per chart. Each follows the same steps: load data, set margins, create the SVG and inner chart group, build scales and axes, then draw shapes and labels.

| Exercise | Chart | Key D3 features |
|---|---|---|
| 5.1 | Vertical bar chart: average energy use of 55-inch TVs by screen type | `d3.scaleBand()`, `d3.axisBottom()`, `d3.axisLeft()` |
| 5.2 | Scatter plot and line chart: average electricity spot price, 1998 to 2024 | `d3.extent()`, `d3.line()`, `d3.format("d")` |
| 5.3 | Donut chart: share of small, medium and large TV models | `d3.pie()`, `d3.arc()`, `arc.centroid()`, `d3.scaleOrdinal()` |

**Results:**
- LCD (LED) and OLED 55-inch TVs use almost the same energy (about 368 kWh a year); LCD uses about 8% less.
- Spot prices stayed between $30 and $66 per MWh until 2015, then rose to a peak of $144.50 in 2022.
- Large TVs (65" and up) make up 45% of models; small TVs (under 43") make up 19%.

---

## Exercise 6 - Interactivity

| Exercise | Feature | File |
|---|---|---|
| 6.1 | Histogram of yearly energy consumption, 14 bins of 200 kWh | `js/histogram.js` |
| 6.2 | Filter buttons (All, LED, LCD, OLED) that update the histogram with a transition | `js/interactions.js` |
| 6.3 | Scatterplot of energy consumption by star rating, coloured by screen type, with a legend | `js/scatterplot.js` |
| 6.4 | Tooltips showing brand, model and screen size when hovering over a dot | `js/interactions.js` |

The code is split the way the exercises describe: `load-data.js` loads the CSV and calls each function, and `shared-constants.js` holds the sizes, colours, scales, bin generator and filter list used by more than one file.

**Results:**
- 60% of TV models use between 200 and 600 kWh a year.
- The median 1-star TV uses 1,135 kWh a year; the median 6-star TV uses 265 kWh.

---

## Data

| File | Used for | Source |
|---|---|---|
| `tv_2026_02_15.csv` | Original data behind 4.x and 5.x | Australian Government Energy Rating register, TV models (February 2026 extract) |
| `ex.csv` | 4.x | TV models counted by brand |
| `tv55ScreenTech.csv` | 5.1 | 55-inch TVs, average energy use by screen type |
| `ARE_Spot_Prices.csv` | 5.2 | Average electricity spot prices by year, supplied for COS30045 |
| `tv_size_count.csv` | 5.3 | TV models counted as Small, Medium or Large |
| `Ex6_TVdata_withStar.csv` | 6.x | Cleaned TV data with star ratings, supplied for COS30045 (prepared with `W6 TV Data.knwf`) |

---

## How to run locally

The pages load CSV files, so they need a local web server.

1. Open the **whole `Exercises` folder** in VS Code (not a single exercise folder, or the links between pages will not work).
2. Right-click `index.html` and choose **Open with Live Server**.
3. Use the navigation bar to move between exercises.

---

## GitHub repositories

Each exercise is submitted as its own GitHub Classroom repository. Copy the contents of the matching folder into each repository.

| Repository | Folder |
|---|---|
| Exercise 4.1 SVG house | `4.1/` |
| Exercises 4.3 to 4.6 Bar chart | `4.x/` |
| Exercise 5 Multi-chart page | `5.x/` |
| Exercise 6 Interactivity | `6.x/` |

---

## Technologies

- HTML, CSS and JavaScript
- [D3.js v7](https://d3js.org/)
- KNIME for data preparation
- Google Fonts: Inter and Space Grotesk

---

## GenAI use

GenAI was used in Exercises 4 to 6. The details are in the GenAI declaration submitted separately on Canvas.
