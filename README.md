import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

def draw_plot():
    # 1. Read data
    df = pd.read_csv('epa-sea-level.csv')

    # 2. Create scatter plot
    fig, ax = plt.subplots(figsize=(10, 6))
    ax.scatter(df['Year'], df['CSIRO Adjusted Sea Level'], label='Observed Data', alpha=0.7)

    # 3. Line of best fit for full dataset
    slope1, intercept1, _, _, _ = linregress(df['Year'], df['CSIRO Adjusted Sea Level'])
    x_pred1 = pd.Series(range(1880, 2051))
    y_pred1 = intercept1 + slope1 * x_pred1
    ax.plot(x_pred1, y_pred1, 'r', label='Best Fit: 1880–2050')

    # 4. Line of best fit from year 2000
    df_recent = df[df['Year'] >= 2000]
    slope2, intercept2, _, _, _ = linregress(df_recent['Year'], df_recent['CSIRO Adjusted Sea Level'])
    x_pred2 = pd.Series(range(2000, 2051))
    y_pred2 = intercept2 + slope2 * x_pred2
    ax.plot(x_pred2, y_pred2, 'g', label='Best Fit: 2000–2050')

    # 5. Labels and title
    ax.set_title('Rise in Sea Level')
    ax.set_xlabel('Year')
    ax.set_ylabel('Sea Level (inches)')
    ax.legend()

    # 6. Save and return
    fig.savefig('sea_level_plot.png')
    return fig
# Sea-Level-Predictor
