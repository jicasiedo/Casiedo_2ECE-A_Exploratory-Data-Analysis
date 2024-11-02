# **Exploratory Data Analysis on Spotify 2023 Dataset Incentive Activity**
## Submitted by: **Jihan Harvey C. Casiedo**
## Section: 2ECE-A
---
## **Background of the Activity 🖼️**
#### Spotify is a digital audio streaming platform for music, podcasts, and videos that allows users to access millions of content from creators around the globe. It has become one of the leading audio streaming platforms, having over 600 million active users as of the second quarter of 2024.
#### Exploratory Data Analysis (EDA) on a dataset featuring popular tracks from the "Most Streamed Spotify Songs 2023." will be conducted in this activity. Using Python functions, we will analyze and investigate the dataset to summarize its characteristics and develop insights into these popular tracks.
---
## **Objectives 🎯** 
### This activity aims to achieve the following:
- **Analyze** the data to identify key information.
- **Visualize** the data for better imaging and understanding.
- **Interpret** the findings to formulate meaningful insights.
---
## General Guidelines 📓
> Given instructions for the activity.
1. Familiarize with the structure of the dataset. Check for missing values and data types. Perform an initial exploration to understand the different features available.
2. Provide summary statistics on key metrics such as streams, release dates, and music attributes (e.g., BPM, danceability).
3. Use appropriate visualizations (bar charts, histograms, scatter plots) to reveal trends and patterns in the data set and ensure clarity by proper labeling. 
4. Identify correlations between different variables. Examine the relationships between streams and other musical characteristics (e.g., tempo, energy, playlists)
5. Offer insights or recommendations regarding popular tracks, artists, or musical trends based on the analysis that can be useful for understanding factors on track popularity.
#### 
---
## **Dataset 💾**
#### The dataset containing the "Most Streamed Spotify Songs 2023" can be downloaded in the *kaggle* website thorugh this link: [Most Streamed Spotify Songs 2023](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023) 🔗
---
## **Activity Proper 📝**
#### Let's import the necessary libraries that we will use in our Python code.
```python
import pandas as pd
import matplotlib.pyplot as plt
```
#### The pandas library is an easy-to-use data structure and data analysis tool for manipulating and analyzing structured data, while the Matplotlib library is used for data visualization. Both of these libraries are the key tools to accomplish this activity.

#### Using the downloaded.csv file containing the "Most Streamed Spotify Songs 2023", we will load the file into spotify_data.
```python
spotify_data = pd.read_csv('spotify-2023.csv')
spotify_data
````
> Output:
