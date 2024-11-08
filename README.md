# **EXPLORATORY DATA ANALYSIS ON SPOTIFY 2023 DATASET**
## Submitted by: **Jihan Harvey C. Casiedo**
## Section: 2ECE-A

---

## **Background of the Activity🖼️**
Spotify is a digital audio streaming platform for music, podcasts, and videos that allows users to access millions of content from creators around the globe. It has become one of the leading audio streaming platforms, having over 600 million active users as of the second quarter of 2024. 

Exploratory Data Analysis (EDA) on a dataset featuring popular tracks from the "Most Streamed Spotify Songs 2023" will be conducted in this activity. Using Python functions, we will analyze and investigate the dataset to summarize its characteristics and develop insights into these popular tracks.

---

## **Objectives 🎯**
  This activity aims to achieve the following:
- **Analyze** the data to identify key information.
- **Visualize** the data for better imaging and understanding.
- **Interpret** the findings to formulate meaningful insights.

---

## General Guidelines 📓
> Given instructions for the activity.
1. Check for missing values and data types.
2. Provide summary statistics on key metrics such as streams, release dates, and music attributes (e.g., BPM, danceability).
3. Visualize trends using bar charts, histograms and scatter plots.
4. Identify correlations between between streams and musical characteristics (e.g., tempo, energy, playlists).
5. Offer insights or recommendations regarding popular tracks, artists, or musical trends based on the analysis.

---

## **Dataset 💾**
  The dataset contains data on the "Most Streamed Spotify Songs 2023" downloadable from the *Kaggle* website through this link: [Most Streamed Spotify Songs 2023](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023) 🔗

---

## **Activity Proper 📝**

### <ins>Importing Libraries</ins>
Import the necessary libraries for data analysis and visualization.
```python
#Import libraries

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

The pandas library is an easy-to-use data structure and data analysis tool for manipulating and analyzing structured data, while the Matplotlib and Seaborn library is used for data visualization. Both of these libraries are the key tools to accomplish this activity.

### <ins>Loading the Dataset</ins>

The "Most Streamed Spotify Songs 2023" dataset is in a `.csv` file and will be loaded in 'spotify_data' dataframe.

```python
#Load the provided dataset into pandas dataframe

spotify_data = pd.read_csv('spotify-2023.csv')
spotify_data
````

> Output:

![image](https://github.com/user-attachments/assets/96f72928-590c-4e52-9cb5-425b606f13fc)

  The `.csv` file displayed a Unicode Decode Error prompt. One of the possible reasons for this is that a different character set is encoded in the file.

  To avoid the encoding errors, we can convert it to a `.xlsx` file by opening the `.csv` file in **Microsoft Excel** and exporting it as a `.xlsx` file.

```python 
spotify_data = pd.read_excel('spotify-2023.xlsx')
spotify_data
```

>Output:
![image](https://github.com/user-attachments/assets/421826ee-8482-4a18-ac10-197348f5d1f4)

### <ins>Adjust Display Settings</ins>

  The dataset has a wide dataframe where some columns are hidden. To display all the columns, adjust the pandas display seeting.

```python
#Adjusting pandas display setting to have a better observation of dataset by being able to view all the columns

pd.set_option('display.max_columns', None)
spotify_data
```

  To revert back to the original pandas display settings:

```python
#Reset pandas display settings

pd.reset_option("all")
spotify_data
```

---

## **Overview of the Dataset 📃**

  In this section, exploratory data analysis will begin by inspecting the shape, data types and missing values of the dataset.

### <ins>Dataset Shape</ins>

  The number of rows and columns of the dataset can be displayed using the `.shape` attribute.

```python
#Display the number of rows and columns of dataframe

print("Number of rows and columns:", spotify_data.shape)
```

>Output:

![image](https://github.com/user-attachments/assets/320aba75-802a-474a-ab38-89da8092d656)

  The dataset has **953 rows** and **24 columns**.

### <ins>Data types of Columns</ins>

  The data types of each column can be displayed by using the `.info()` attribute.

```python
#Extract the data tyoes of each column in the dataframe

spotify_data.info()
```

>Output:

![image](https://github.com/user-attachments/assets/65f4d8bb-529a-4220-8e15-7a13e74ba9da)

  Summary of the data types of columns:

  Integer (18 items): Artist Count, Released Year, Released Month, Released Day, In Spotify Playlists, In Spotify Charts, In Apple Playlists, In Apple Charts, In Deezer Playlists, In Deezer Charts, Bpm, Danceability %, Valence %, Energy %, Acousticness %, Instrumentalness %, Liveness %, and Speechiness %.
  Float (1 item): In Shazam Charts
  Object (5 items): Track Name, Artist(s) Name, Streams, Key, Mode.

### <ins>Missing Values in the Dataset</ins>

  The `.info()` attribute displayed the number of non-empty cells in each column. The columns of in_shazam_chart and key has missing values.

  Alternatively, the number of missing values of each column by using this method:

```python
#Count the missing values of a column

rows = len(spotify_data)
not_missing = spotify_data.count()
missing = rows - not_missing
missing [missing > 0]
```

>Output:

![image](https://github.com/user-attachments/assets/357660d9-a187-4411-bd87-663f7e04f96b)

  The `.len()` function counted the number of rows of the dataset and the `.count()` function counted the non-missing values in the dataset. 

  The number of missing values is calculated by subtracting the non-missing values of each row from the number of rows. 

  The syntax `missing [missing > 0]` filters out to display only the columns with missing values more than 0.

  The **"key"** column have 95 missing values** while the **"in_shazem_charts"** column have 50 missing values"**.

---

## **Basic Descriptive Statistics 📊**

  In this section, the mean, median, and standard deviation of the dataset is calculated and the distribution of released year and artist count is visualized


### <ins>Streams Column Conversion

  The streams column is an object as displayed the overview of the dataset.
  The column can be converted into numeric values using the `pd.to_numeric()` function.

```python
#Convert the object column to numeric values

streams = pd.to_numeric(spotify_data['streams'], errors='coerce')
streams
```

>Output: 

![image](https://github.com/user-attachments/assets/e566f087-6223-45d6-a28c-3ec7b7999cdc)

The `errors='coerce'` is made to set the non-convertible values to numeric will be replaced with NaN.

### **<ins>Mean</ins>**

  The mean can be calculated using the `.mean()` attribute and `round` function to display the mean in two decimal places.

```python
#Calculate the mean

mean = round(streams.mean(),2)
mean
```

>Output:
![image](https://github.com/user-attachments/assets/bcda3e1d-bd8e-4867-96cd-a8398c67e51d)

  The average stream value of the "Most Streamed Spotify Songs 2023" dataset is 514,137,424.94 streams.

### **<ins>Median</ins>**

  The median can be identified using the `.mean()` attribute and `round` function to display the median in two decimal places.

```python
#Calculate the median

median = round(streams.median(),2)
median
```

>Output:
![image](https://github.com/user-attachments/assets/24c7dca1-8a88-4ebf-ac89-f3b7ec83937e)

  The median value of the streams in the "Most Streamed Spotify Songs 2023" dataset is 290,530,915 streams.

### **<ins>Standard Deviation</ins>**

  The standard deviation can be calculated using the `.std()` attribute and `round` function to display the standard deviation in two decimal places.

```python
#Calculate the standard deviation

std = round(streams.std(),2)
std
```

>Output:
![image](https://github.com/user-attachments/assets/3d616347-15d6-40f9-9dc4-2f40270e5c7b)

  The standard deviation of the streams of the "Most Streamed Spotify Songs 2023" dataset is 566,856,949.04 streams. 

### <ins>Observation</ins>

  The standard deviation has a higher value compared to the mean, indicating that there is a wide range in streaming data. This suggests that there are tracks that are significantly more streamed than others.

### **<ins>Distribution of Released Year and Artist Count</ins>**

  The graphical representation to be used for data visualization are histograms. The visualization can be achieved with the Matplotlib library using the following:

  `plt.figure(figsize=( , ))` for the figure size
  `plt.hist` to generate a histogram
  `plt.title` for the graph title
  `plt.xlabel()` for the label on x-axis
  `plt.ylabel()` for the label on y-axis
  `plt.show()` to display the graph

```python
# Plot the distribution of 'released_year'

plt.figure(figsize=(18, 9))
plt.hist(spotify_data['released_year'],)
plt.title('Distribution of Released Year')
plt.xlabel('Released Year')
plt.ylabel('Count')
plt.show()

# Plot the distribution of 'artist_count'

plt.figure(figsize=(18,9))
plt.hist(spotify_data['artist_count'])
plt.title('Distribution of Artist Count')
plt.xlabel('Artist Count')
plt.ylabel('Count')
plt.show()
```

>Output:

![image](https://github.com/user-attachments/assets/10f611bd-d4a8-4604-9528-a18268e36afb)

### <ins>Observation</ins>

  The histogram of the released year shows that most of the tracks in the dataset are those released in the 2020s, and most of the tracks also have only one artist followed by two artists, and tracks with many more artists appear less.

---

## **Top Performers 🕺**

  In this section, the top streamed tracks and most frequent artists from the "Most Streamed Spotify Songs 2023" dataset are identified.

### <ins>Top 5 Most Streamed Tracks</ins> 🎧

### <ins>Sort Data by Streams

  The rows can be sorted using the `.sort_values(by = 'streams', ascending = False])` The `ascending = False` makes the list to be displayed in descending order (highest to lowest)

  The `.head()` function to display the top 5 of the list.

```python
#Sort the streams dataframe by number of streams in descending order (highest to lowest)

spotify_data['streams'] = pd.to_numeric(spotify_data['streams'], errors='coerce')
sorted_stream = spotify_data.sort_values(by='streams', ascending=False)

#Display the top 5 artists

sorted_stream.head()
```

>Output:
![image](https://github.com/user-attachments/assets/1542e872-3735-414e-82d2-380cb7a54410)

  The most streamed track on Spotify during 2023 is **Blinding Lights** by The Weeknd, with 3,703,895,074 streams.

### <ins>Top Artists</ins> 🎤

  The `.valuecounts()` function counts the number of appearances of artists.
  The `.head()` function displays the top 5 most frequent artists.

```python
#Count the appearances of the top 5 artists

artist_count = spotify_data['artist(s)_name'].value_counts()
artist_count.head()
```

>Output:
![image](https://github.com/user-attachments/assets/d6872024-8586-41d2-872f-0b1142dbd6d4)

  The top five most frequent artists are Taylor Swift with 34 songs, The Weeknd with 22 songs, Bad Bunny with 19 songs, Sza with also 19 songs, and Harry Styles with 17 songs.

---

## Temporal Trends 📈

  In this section, the trends in the number of tracks based on its year of release and month of release is observed and analyze.

### <ins>Tracks and Released Year</ins> 📅

  The `.valuecounts()` function counts the number of appearances of artists.
  The `.sort_index()` attribute sorts by labels along the x-axis.

  The graphical representation to be used for data visualization is the bar graph. The visualization can be achieved with the Matplotlib library using the following:
  `plt.figure(figsize=( , ))` for the figure size
  `plt.title` for the graph title
  `plt.xlabel()` for the label on x-axis
  `plt.ylabel()` for the label on y-axis
  `plt.grid(axis='y')` to generate the gridlines for better viewing
  `plt.show()` to display the graph

```python
#Display the number of tracks released per year in the dataset

tracks_year = spotify_data['released_year'].value_counts().sort_index()

plt.figure(figsize=(12, 6))
tracks_year.plot(kind='bar')
plt.title('No. of Tracks Released Per Year')
plt.xlabel('Year')
plt.ylabel('No. of Tracks Released')
plt.grid(axis='y')
plt.show()
```

>Output:

![image](https://github.com/user-attachments/assets/82619904-819f-4bbe-b3cb-b9f6dd6573e4)

### <ins>Observation</ins>

  The graph displays that the release year 2022 has the highest number of tracks in the "Most Streamed Spotify Songs 2023" list, followed by songs released in 2023. This suggests that popular songs from the previous year o being heavily streamed over time, most likely giving them higher streams compared to latest releases. This could explain why songs released in 2023 have fewer streams because of the less time to accumulate listeners. A similar pattern may continue, that the previous year has more tracks in stream rankings than those released in the ranking year.

  Another thing to notice is that there are songs in the dataset that were released significantly earlier. This suggests that it is possible that classic hits from the past are still attracting listeners up until now. This highlights that there are certain songs that last in terms of popularity that traverse through time.

### <ins>Tracks and Released Month</ins> 🕒

  The `.valuecounts()` function counts the number of appearances of artists.
  The `.sort_index()` attribute sorts by labels along the x-axis.

  The graphical representation to be used for data visualization is the bar graph. The visualization can be achieved with the same method from the *No. of Tracks Released Per Year* graph.

```python
#Display the number of tracks released per month in the dataset

tracks_month = spotify_data['released_month'].value_counts().sort_index()
plt.figure(figsize=(15, 8))
tracks_month.plot(kind='bar')
plt.title('No. of Tracks Released Per Month')
plt.xlabel('Year')
plt.ylabel('No. of Tracks Released')
plt.grid(axis='y')
plt.show()
```

>Output:
![image](https://github.com/user-attachments/assets/51ebdc26-df27-49cf-b68e-39a2c5e3f7c9)

### <ins>Observation</ins>

  The graph displays that the month of January has the highest number of tracks releases in the "Most Streamed Spotify Songs 2023" list, followed by month of May. The tracks released in January might be a strategic method  since those have potential to accumulate more streams for the rest of the year. 

  Each of the months has an adequate number of track releases throughout the year. This shows that the music industry and music interest remains present all year round.

---

##  Genre and Music Characteristics 🎶

  In this section, the correlation between streams and different attributes present in the dataset is observed and analyzed.

  An ideal data visualization of the correlation of different attributes can be best represented with the use of heatmaps. Heatmaps are visual tools that makes identifying patterns, trends, or correlations easier to interpret.

  The heatmap visualization can be achieved using the following:
  `plt.figure(figsize=( , ))` for the figure size
  `plt.title` for the graph title
  `sns.heatmap` for the type of graph
  `annot` = True` to display numerical value
  `cmap='coolwarm` to adjust the colors of the graph
  `plt.show()` to display the graph

```python
#Group the track characteristics in the dataset

characteristics = spotify_data[['streams', 'bpm', 'danceability_%', 'valence_%',	'energy_%',	'acousticness_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%']].corr()

#Plotting the heatmap

plt.figure(figsize=(12, 10))
sns.heatmap(characteristics, annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap between Streams and Musical Attributes")
plt.show()
```

>Output:
![image](https://github.com/user-attachments/assets/3cf160cc-35d9-41bf-a060-9a9e48fbbf27)

### <ins>Observation</ins>

  The heatmap displayed a weak relationship of streams with other attributes. No single musical characteristic seems to influence the number of streams a track has. This indicates that popular songs do not rely on a single characteristic.

  The attributes that showed a noticeable correlation are "danceability" with "valence" and "energy" with "valence" as well. The "energy" and "acousticness" showed the weakest correlation among the attributes. This indicates that the higher the acousticness of the song, the less energy it gives off, and vice versa.

---

## **Platform Popularity 💹** 

  In this section, the Spotify and Apple platform are compared to identify which platform favors the most popular tracks by analyzing the number of tracks in user playlists and charts.

  The `.mean()` attribute is used to calculate the average number of tracks in user playlists and charts for both platforms.

```python
#Calculate the mean of playlists and charts

ave_spotify_playlists = spotify_data['in_spotify_playlists'].mean()
ave_spotify_charts = spotify_data['in_spotify_charts'].mean()
ave_apple_playlists = spotify_data['in_apple_playlists'].mean()
ave_apple_charts = spotify_data['in_apple_charts'].mean()

#Group the averages and label them

averages = [ave_spotify_playlists, ave_spotify_charts, ave_apple_playlists, ave_apple_charts]
labels = ['Spotify Playlists', 'Spotify Charts', 'Apple Playlists', 'Apple Charts']

# Plotting the bar graph

plt.figure(figsize=(13, 10))
plt.bar(labels, averages)
plt.ylabel('Average Number')
plt.title('Average of Tracks Appearing in Spotify and Apple Playlists and Charts')
plt.show()
```

> Output:
![image](https://github.com/user-attachments/assets/6a88eee3-8056-4df6-a03c-e65892085f4f)

### <ins>Observation</ins>

  The graph showed an overwhelming number of tracks being included in playlists for Spotify users, but the tracks appear lower in charts, while the tracks in the Apple platform displayed much fewer appearances in playlists and charts.

  We can conclude that Spotify is the more favored platform in the most popular tracks having a large number of the tracks being included in playlists.

---

## **Advanced Analysis 💭** 

  In this section, other possible contributing factors to the number of streams such as keys, modes and artists.
 
### <ins>Streams and Keys</ins> 🎵

  The `.groupby` function groups the numbers of streams by its key.
  The `.mean()` function calculated the average number of streams per key.
  The `.reset_index()` is used so that the results can be used further.


```python
#Group the keys and their average number of streams

key_analysis = spotify_data.groupby('key')['streams'].mean().reset_index()

#Plotting the bar graph

plt.figure(figsize=(12, 6))
plt.bar(key_analysis['key'], key_analysis['streams'])
plt.title('Average Streams by Key')
plt.ylabel('Average Streams')
plt.xlabel('Key')
plt.show()
```

>Output:
![image](https://github.com/user-attachments/assets/38c08138-cb34-4539-9f14-b6895bcc6255)

### <ins> Streams and Modes</ins>🎵

  The `.groupby` function groups the numbers of streams by its key.
  The `.mean()` function calculated the average number of streams per key.
  The `.reset_index()` is used so that the results can be used further.

```python
#Group the modes and their average number of streams

mode_analysis = spotify_data.groupby('mode')['streams'].mean().reset_index()

#Plotting the bar graph

plt.figure(figsize=(12, 6))
plt.bar(mode_analysis['mode'], mode_analysis['streams'])
plt.title('Average Streams by Mode')
plt.ylabel('Average Streams')
plt.xlabel('Mode')
plt.show()
```

>Output:
![image](https://github.com/user-attachments/assets/f519d380-6536-4753-85fe-66faa44c109b)

### <ins>Observation</ins>

  The graphs for the relationship between streams, keys, and modes suggest that the songs with the major keys tend to have a slightly higher average number of streams. This tells us that the key and major of a song do not strongly affect the number of streams or popularity.

### <ins>Genres and Artists</ins> 🧑‍🎤

  The total number of playlists and charts of Spotify and Apple is combined.

```python
#Make new columns with the total of the playlist and chart appearances in Spotify and Apple

spotify_data['total_playlist'] = spotify_data['in_spotify_playlists'] + spotify_data['in_apple_playlists']
spotify_data['total_chart'] = spotify_data['in_spotify_charts'] + spotify_data['in_apple_charts']

#Group the Artist(s) and their total playlist and chart appearances and display in descending order (highest ot lowest)

artist_analysis = spotify_data.groupby('artist(s)_name')[['total_playlist', 'total_chart']].sum().reset_index()
artist_analysis = artist_analysis.sort_values(by=['total_playlist', 'total_chart'], ascending=False)

#Display the top 10 artists

top_10_artists = artist_analysis.head(10)

#Plotting the bar graph for streams and playlist appearances of top artists

plt.figure(figsize=(12, 6))
plt.bar(top_10_artists['artist(s)_name'], top_10_artists['total_playlist'], label='Playlist Appearances')
plt.title('Top 10 Artists by Playlist Appearance')
plt.ylabel('Total Appearances')
plt.xlabel('Artist')
plt.show()

#Plotting the bar graph for streams and chart appearances of top artists

plt.figure(figsize=(12, 6))
plt.bar(top_10_artists['artist(s)_name'], top_10_artists['total_chart'], label='Chart Appearances')
plt.title('Top 10 Artists by Chart Appearance')
plt.ylabel('Total Appearances')
plt.xlabel('Artist')
plt.show()
```

>Output:

![image](https://github.com/user-attachments/assets/ee3cae6a-cd64-45eb-8ed3-cf6d1087d8cc)

### <ins>Observation</ins>

  The ranking of top artists differs between playlists and chart appearances. The Weeknd leads in playlist appearances, followed by Taylor Swift, Ed Sheeran, and Harry Styles. This suggests that the tracks of The Weeknd are frequently included on playlists. 

  However, Taylor Swift ranks highest in chart appearances, with about a thousand more than The Weeknd. This suggests that despite being second in terms of playlist appearance, Taylor Swift’s tracks perform better in terms of sales, making her higher in chart rankings.
## **Conclusion**

Exploratory data analysis on the most streamed songs on Spotify in 2023 provided meaningful insights into the trends and factors that contribute to the success and popularity of tracks. By analyzing the data, the key trend are identify and through data visualization, data analysis becomes much easier. Data gathered from the analysis can guide future studies on music trends and artist success. To gain a deeper understanding, comparing data across multiple years allows a more comprehensive analysis, offering clearer insights of the trends and patterns of track popularity.

To have a more in depth analysis, comparison of the data gathered across the years can help provide a better understanding and more accurate observations in studying the popularity of tracks.
