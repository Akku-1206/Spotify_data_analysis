Spotify Tracks Analysis
Overview
This project performs an exploratory data analysis (EDA) on Spotify music data to uncover insights and correlations related to song features, popularity, and genre. The code provided utilizes Python and popular data science libraries like Pandas, Seaborn, and Matplotlib to perform data cleaning, manipulation, and visualization.

The main objectives of this analysis are:

Identifying popular songs and genres.
Understanding correlations between different song attributes.
Analyzing trends over time, including song duration and release years.
Requirements
To run this project, you need:

Python 3.x
Libraries: numpy, pandas, matplotlib, seaborn
To install the required libraries, use:

bash
Copy code
pip install numpy pandas matplotlib seaborn
Dataset
The project uses two datasets:

tracks.csv: Contains details of Spotify tracks, including features like popularity, duration, and release date.
SpotifyFeatures.csv: Provides information on genre-specific features.
Code Walkthrough
Data Loading and Cleaning

Loads tracks.csv and SpotifyFeatures.csv into Pandas DataFrames.
Cleans the release_date column in tracks.csv to ensure uniform date formatting.
Converts duration_ms into seconds for easier interpretation.
Data Exploration

Checks for null values and displays summary statistics.
Sorts and displays the 10 least popular tracks.
Feature Engineering

Adds a years column from the release date.
Converts track duration from milliseconds to seconds.
Correlation Analysis

Creates a heatmap to show correlations between numeric attributes of songs.
Plots regression between features, such as loudness vs. energy and popularity vs. acousticness.
Visualization of Trends

Plots the distribution of song releases by year.
Analyzes the duration of songs over the years.
Genre Analysis

Compares the duration and popularity of songs across different genres.
Key Code Sections
Data Cleaning

python
Copy code
tracks.reset_index(inplace=True)
tracks = tracks[tracks['release_date'].str.match(r'^\d{4}-\d{2}-\d{2}$', na=False)]
tracks.set_index("release_date", inplace=True)
tracks.index = pd.to_datetime(tracks.index)
Correlation Heatmap

python
Copy code
corr_tracks = tracks.drop(["key", "mode", "explicit"], axis=1).select_dtypes(include=[float, int]).corr(method="pearson")
plt.figure(figsize=(14, 6))
sns.heatmap(corr_tracks, annot=True, fmt=".1g", vmin=-1, vmax=1, center=0, cmap="inferno")
plt.show()
Top Genre by Popularity

python
Copy code
famous = genre.sort_values("popularity", ascending=False).head(10)
sns.barplot(y='genre', x='popularity', data=famous).set(title="Top 5 Genre by popularity")
Results
Popular Songs and Genres: Displays the most popular tracks and top genres by popularity.
Trends Over Time: Analyzes the release trend of songs over the years.
Correlation Insights: Highlights the relationships between different song features.
File Outputs
zomato_restaurants.csv: Final CSV file containing the cleaned and processed Spotify data for further analysis or sharing.
