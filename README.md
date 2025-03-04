# sea-level-project1
import pandas as pd
import matplotlib.pyplot as plt
import scipy.stats as stats

def draw_plot():
    # Load data
    df = pd.read_csv("epa-sea-level.csv")

    # Create scatter plot
    plt.figure(figsize=(10, 6))
    plt.scatter(df["Year"], df["CSIRO Adjusted Sea Level"], label="Data", alpha=0.6)

    # First regression line (1880 - 2050)
    slope1, intercept1, _, _, _ = stats.linregress(df["Year"], df["CSIRO Adjusted Sea Level"])
    years1 = range(1880, 2051)
    sea_levels1 = [slope1 * year + intercept1 for year in years1]
    plt.plot(years1, sea_levels1, "r", label="Best Fit (1880-2050)")

    # Second regression line (2000 - 2050)
    df_recent = df[df["Year"] >= 2000]
    slope2, intercept2, _, _, _ = stats.linregress(df_recent["Year"], df_recent["CSIRO Adjusted Sea Level"])
    years2 = range(2000, 2051)
    sea_levels2 = [slope2 * year + intercept2 for year in years2]
    plt.plot(years2, sea_levels2, "g", label="Best Fit (2000-2050)")

    # Labels and title
    plt.xlabel("Year")
    plt.ylabel("Sea Level (inches)")
    plt.title("Rise in Sea Level")
    plt.legend()

    # Save figure
    plt.savefig("sea_level_plot.png")
    return plt.gca()

# Run the function
if __name__ == "__main__":
    draw_plot()
