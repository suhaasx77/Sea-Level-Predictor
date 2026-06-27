# Sea-Level-Predictor

```python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress
import numpy as np


def draw_plot():
    # Read data
    df = pd.read_csv("epa-sea-level.csv")

    # Create scatter plot
    fig, ax = plt.subplots(figsize=(10, 6))
    ax.scatter(df["Year"], df["CSIRO Adjusted Sea Level"])

    # First line of best fit (1880 - latest year)
    result = linregress(df["Year"], df["CSIRO Adjusted Sea Level"])

    years = np.arange(df["Year"].min(), 2051)

    ax.plot(
        years,
        result.intercept + result.slope * years,
        color="red"
    )

    # Second line of best fit (2000 - latest year)
    df_recent = df[df["Year"] >= 2000]

    result_recent = linregress(
        df_recent["Year"],
        df_recent["CSIRO Adjusted Sea Level"]
    )

    years_recent = np.arange(2000, 2051)

    ax.plot(
        years_recent,
        result_recent.intercept + result_recent.slope * years_recent,
        color="green"
    )

    # Labels and title
    ax.set_xlabel("Year")
    ax.set_ylabel("Sea Level (inches)")
    ax.set_title("Rise in Sea Level")

    # Save plot and return figure
    fig.savefig("sea_level_plot.png")
    return fig
```

---

## `main.py`

```python
from sea_level_predictor import draw_plot

draw_plot()
```

---

## Concepts Used

* `pd.read_csv()`
* `plt.scatter()`
* `scipy.stats.linregress()`
* `numpy.arange()`
* Linear regression (line of best fit)
* Filtering rows with Boolean indexing
* `plt.plot()`
* `set_xlabel()`
* `set_ylabel()`
* `set_title()`

---

### Project Workflow

1. Read `epa-sea-level.csv` into a Pandas DataFrame.
2. Create a scatter plot of:

   * **X-axis:** `Year`
   * **Y-axis:** `CSIRO Adjusted Sea Level`
3. Compute the **first regression line** using all available data (1880–latest year) and extend it to **2050**.
4. Compute the **second regression line** using only data from **2000 onward** and extend it to **2050**.
5. Label the axes:

   * **X-axis:** `Year`
   * **Y-axis:** `Sea Level (inches)`
6. Set the title to **"Rise in Sea Level"**.
7. Save the plot as **`sea_level_plot.png`** and return the figure.

This implementation satisfies all the freeCodeCamp project requirements and passes the official unit tests.
