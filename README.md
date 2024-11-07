# **Exploratory Data Analysis on Spotify 2023 Dataset Incentive Activity**
## Submitted by: **Jihan Harvey C. Casiedo**
## Section: 2ECE-A

---

## **Background of the Activity 🖼️**
#### Spotify is a digital audio streaming platform for music, podcasts, and videos that allows users to access millions of content from creators around the globe. It has become one of the leading audio streaming platforms, having over 600 million active users as of the second quarter of 2024. 

#### Exploratory Data Analysis (EDA) on a dataset featuring popular tracks from the "Most Streamed Spotify Songs 2023" will be conducted in this activity. Using Python functions, we will analyze and investigate the dataset to summarize its characteristics and develop insights into these popular tracks.

---

## **Objectives 🎯**
#### This activity aims to achieve the following:
- **Analyze** the data to identify key information.
- **Visualize** the data for better imaging and understanding.
- **Interpret** the findings to formulate meaningful insights.

---

## General Guidelines 📓
> Given instructions for the activity.
1. Familiarize yourself with the structure of the dataset. Check for missing values and data types. Perform an initial exploration to understand the different features available.
2. Provide summary statistics on key metrics such as streams, release dates, and music attributes (e.g., BPM, danceability).
3. Use appropriate visualizations (bar charts, histograms, scatter plots) to reveal trends and patterns in the dataset, ensuring clarity with proper labeling.
4. Identify correlations between different variables. Examine the relationships between streams and other musical characteristics (e.g., tempo, energy, playlists).
5. Offer insights or recommendations regarding popular tracks, artists, or musical trends based on the analysis, which can be useful for understanding factors affecting track popularity.

---

## **Dataset 💾**
#### The dataset containing the "Most Streamed Spotify Songs 2023" can be downloaded from the *Kaggle* website through this link: [Most Streamed Spotify Songs 2023](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023) 🔗

---

## **Activity Proper 📝**
#### Let's import the necessary libraries that we will use in our Python code.
```python
#Import the necessary libraries to be used in the activity (pandas and matplotlib)

import pandas as pd
import matplotlib.pyplot as plt
```

#### The pandas library is an easy-to-use data structure and data analysis tool for manipulating and analyzing structured data, while the Matplotlib library is used for data visualization. Both of these libraries are the key tools to accomplish this activity.

#### Using the downloaded `.csv` file containing the "Most Streamed Spotify Songs 2023", we will load the file into 'spotify_data'.
```python
#Load the provided dataset into pandas dataframe

spotify_data = pd.read_csv('spotify-2023.csv')
spotify_data
````
> Output:

![image](https://github.com/user-attachments/assets/96f72928-590c-4e52-9cb5-425b606f13fc)

#### After loading the file, it showed a Unicode Decode Error prompt. One of the reasons for this is that a different character set is encoded in the file.

#### One method we can use to load the dataset is to launch the `.csv` file in our device, open it in **Microsoft Excel** and export it as a `.xlsx` file.

#### Now, we load the file again in our code into `spotify_data`.
```python 
spotify_data = pd.read_excel('spotify-2023.xlsx')
spotify_data
```
>Output:
![image](https://github.com/user-attachments/assets/421826ee-8482-4a18-ac10-197348f5d1f4)

#### In this output, the dataset has a wide dataframe where some columns are hidden. We can display all the columns by changing the pandas display settings with this code:
```python
#Adjusting pandas display setting to have a better observation of dataset by being able to view all the columns

pd.set_option('display.max_columns', None)
spotify_data
```

#### To revert back to the original pandas display settings, this code is to be used:
```python
#Reset pandas display settings

pd.reset_option("all")
spotify_data
```

---

## **Overview of the Dataset 📃**

#### We can begin the exploratory data analysis now that we can see our dataset.

#### The size or dimension of our dataset can be known using the `.shape` attribute.
```python
#Display the number of rows and columns of dataframe

print("Number of rows and columns:", spotify_data.shape)
```

>Output:

![image](https://github.com/user-attachments/assets/320aba75-802a-474a-ab38-89da8092d656)

#### The dataset has **953 rows** and **24 columns**.

#### Now, let's get the information of our dataset. We will use the `.info()` attribute to identify the data types of each column of the dataset.

```python
#Extract the data tyoes of each column in the dataframe

spotify_data.info()
```

>Output:
![image](https://github.com/user-attachments/assets/65f4d8bb-529a-4220-8e15-7a13e74ba9da)

#### With this, we can see the data types of each column, and additionally, the number of non-empty cells in each column is displayed.

#### Here is a summary of the data types:

#### Integer (18 items): Artist Count, Released Year, Released Month, Released Day, In Spotify Playlists, In Spotify Charts, In Apple Playlists, In Apple Charts, In Deezer Playlists, In Deezer Charts, Bpm, Danceability %, Valence %, Energy %, Acousticness %, Instrumentalness %, Liveness %, and Speechiness %.
#### Float (1 item): In Shazam Charts
#### Object (5 items): Track Name, Artist(s) Name, Streams, Key, Mode.

#### Observing the number of non-empty cells in each column displayed using the .info() attribute, we can say that the columns of in_shazam_chart and key has missing values.

#### Alternatively, we can count the number of missing values of each column by using another method:
```python
#Count the missing values of a column

rows = len(spotify_data)
not_missing = spotify_data.count()
missing = rows - not_missing
missing [missing > 0]
```

>Output:

![image](https://github.com/user-attachments/assets/357660d9-a187-4411-bd87-663f7e04f96b)

#### In this code, the columns with missing values and the missing values are displayed. This is achieved first by counting the rows using the `.len()` function and `.count()` function to count the non-missing values in the dataset. Subtracting the number of missing values from the number of rows gives us the missing values in the dataset. Lastly. the syntax inside the bracket is made to filter out to display only the columns with missing values more than 0.

#### The results displayed that **"key" column having 95 missing values** and **"in_shazem_charts" column having 50 missing values"**.

---

## **Basic Descriptive Statistics 📊**

#### In this section, we will explore basic descriptive statistics of the streams of the songs in the dataset by calculating its mean, median, and standard deviation to understand the average number of streams, the middle ground of streams, and the variation in streaming activity. These statistics will provide a better understanding of the dataset.

### **Mean**

#### Going back to the overview of the dataset, we discovered that the streams column is an object but we need it to be in numerical value so that we can calculate its mean.

#### Let's convert the datatype of the streams column:
```python
#Convert the object column to numeric values

streams = pd.to_numeric(spotify_data['streams'], errors='coerce')
streams
```

>Output: 

![image](https://github.com/user-attachments/assets/e566f087-6223-45d6-a28c-3ec7b7999cdc)

#### We can now calculate the mean of the streams column using the `.mean()` attribute and `round` function to make our mean in two decimal places.
```python
#Calculate the mean

mean = round(streams.mean(),2)
mean
```

>Output:
![image](https://github.com/user-attachments/assets/bcda3e1d-bd8e-4867-96cd-a8398c67e51d)

#### The average stream value of the "Most Streamed Spotify Songs 2023" dataset is 514,137,424.94.

### **Median**

#### We can get the median of the streams column by using the `.median()` attribute:
```python
#Calculate the median

median = round(streams.median(),2)
median
```

>Output:
![image](https://github.com/user-attachments/assets/24c7dca1-8a88-4ebf-ac89-f3b7ec83937e)

#### The median value of the streams in the "Most Streamed Spotify Songs 2023" dataset is 290,530,915.


### **Standard Deviation**

#### We will use the `.std()` attribute to compute the standard deviation of the streams column and `round()` function to make our result in two decimal places:
```python
#Calculate the standard deviation

std = round(streams.std(),2)
std
```

>Output:
![image](https://github.com/user-attachments/assets/3d616347-15d6-40f9-9dc4-2f40270e5c7b)

#### The standard deviation of the streams of the "Most Streamed Spotify Songs 2023" dataset is 566,856,949.04. 

#### We can notice that the standard deviation value is higher than the mean. This tells us that the range of stream data varies greatly indicating that some songs are significantly more popular than others.

### **Distribution**

---

## **Top Performers 🕺**

#### In this section, we will identify the top streamed tracks and most frequent artists from the "Most Streamed Spotify Songs 2023" dataset.


### Top 5 Most Streamed Track 🎧

#### To identify the top streamed tracks of the dataset we will use `.sort_values(by = 'streams', ascending = False]` attribute to sort the tracks by number of streams in descending order and `.head()` function to display the top 5 of the list.
```python
#Sort the streams dataframe by number of streams in descending order (highest to lowest)

sorted_stream = spotify_data.sort_values(by='streams', ascending=False)

#Display the top 5 artists

sorted_stream.head()
```

>Output:
![image](https://github.com/user-attachments/assets/1542e872-3735-414e-82d2-380cb7a54410)

#### The most streamed track in Spotify during 2023 is **Blinding Lights** by The Weeknd with 3,703,895,074 streams.

### Top Artists 🎤

#### To count the frequency of each artists in the dataset, the `.valuecounts()` function and the `.head()` is used to display the top 5 most frequent artists.
```python
#Count the appearances of the top 5 artists

artist_count = spotify_data['artist(s)_name'].value_counts()
artist_count.head()
```

>Output:
![image](https://github.com/user-attachments/assets/d6872024-8586-41d2-872f-0b1142dbd6d4)

#### Here we can see that that the top five most frequent artists are Taylor Swift with 34 songs, The Weeknd with 22 songs, Bad Bunny with 19 songs, Sza with also 19 songs, and Harry Styles with 17 songs.

---

## Temporal Trends 📈

#### In this section, we will analyze the trends in the number of tracks based on its year of release and month of release. Observation on the visualization that will be produced will help generate insights and ideas id and how time contributes to the number of streams of Spotify songs during 2023.

### Tracks and Released Year 📅

#### To organize the tracks in the dataset to its year of release we will use the `.sort_index()` attribute to sort by labels along the x-axis.

#### The graphical representation to be used for data visualization is the bar graph. The visualization can be achieved with the Matplotlib library using the following:
#### `plt.figure(figsize=( , ))` for the figure size
#### `plt.title` for the graph title
#### `plt.xlabel()` for the label on x-axis
#### `plt.ylabel()` for the label on y-axis
#### `plt.grid(axis='y')` to generate the gridlines for better viewing
#### `plt.show()` to display the graph
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

#### The graph displays that release year 2022 has the highest number of tracks in the "Most Streamed Spotify Songs 2023" list, followed by songs released on 2023. This suggests that popular songs from the previous year o being heavily streamed over time, most likely giving them higher streams compared to latest releases. This could explain why songs released in 2023 have lesser streams because of the lesser time to accumulate listeners. A similar pattern may continue, that the previous year has more tracks in stream rankings than those released in the ranking year.

#### Another thing to notice is that there are songs in the dataset that were released significantly earlier. This suggests that it is possible that classic hits from the past are still attracting listeners up until now. This highlights that there are certain songs that lasts in terms of popularity that traverse through time.

### Tracks and Released Month 🕒

#### To organize the tracks in the dataset to its month of release we will use the `.sort_index()` attribute to sort by labels along the x-axis.

#### The graphical representation to be used for data visualization is the bar graph. The visualization can be achieved with the same method from the *No. of Tracks Released Per Year* graph.
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

#### The graph displays that the month of January has the highest number of tracks releases in the "Most Streamed Spotify Songs 2023" list, followed by month of May. The tracks released in January might be a strategic method  since those have potential to accumulate more streams for the rest of the year. 

#### Each of the months has an adequate number of track releases throughout the year. This shows that the music industry and music interest remains present all year round.

---

##  Genre and Music Characteristics 🎶

#### In this section, we will observe and analyze the correlation of different attributes present in the dataset on how it contributes to the number of streams.

#### An ideal data visualization of correlation of different attributes can be best represented with the use of heatmaps. Heatmaps are visual tools that makes identifying patterns, trends, or correlations easier to interpret.

#### Seaborn library will be used for better graphics on the data visualization of correlations
```python 
#Import seaborn, another data visualization library

import seaborn as sns
```

The visualization can be achieved using the following:
#### `plt.figure(figsize=( , ))` for the figure size
#### `plt.title` for the graph title
#### `sns.heatmap` for the type of graph
#### `annot` = True` to display numerical value
#### `cmap='coolwarm` to adjust the colors of the graph
#### `plt.show()` to display the graph

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

#### The heatmap displayed a weak relationship of streams with other attributes. No single musical characteristic seems to influence the number of streams a track has. This indicates that popular songs do not rely on a single characteristic.

#### The attributes that showed a noticeable correlation are "danceability" with "valence" and "energy" with "valence" as well. The "energy" and "acousticness" showed the weakest correlation among the attributes. This indicates that the higher the acousticness of the song, the less energy it gives off, and vice versa.

---

## **Platform Popularity 💹** 

#### In this section. we will identify what music platform favors the most popular tracks.

#### To identify the how frequent the tracks in the dataset appear in the charts and playlists in Spotify and Apple, we will get the average of each column and compare the results

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

#### The graph showed an overwhelming number of tracks being included in playlists for Spotify users, but the tracks appear lower in charts, while the tracks in the Apple platform displayed much fewer appearances in playlists and charts.

#### We can conclude that Spotify is the more favored platform in the most popular tracks having a large number of the tracks being included in playlists.

---

## **Advanced Analysis 💭** 

#### In this section. we will identify other possible contributing factors to the number of streams of a track from the "Most Streamed Songs in Spotify 2023" dataset.
 
### Streams and Keys 🎵

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

### Modes and Keys 🎵

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

#### The graphs for the relationship between streams, keys, and modes suggest that the songs with the major keys tend to have a slightly higher average number of streams. This tells us that the key and major of a song do not strongly affect the number of streams or popularity.

### Genres and Artists 🧑‍🎤

```python
#Total the playlist and chart appearances in Spotify and Apple

playlists = spotify_data['in_spotify_playlists'] + spotify_data['in_apple_playlists']
spotify_data['total_chart_appearances'] = spotify_data['in_spotify_charts'] + spotify_data['in_apple_charts']

#Group the Artist(s) and their total playlist and chart appearances and display in descending order (highest ot lowest)

artist_analysis = spotify_data.groupby('artist(s)_name')[['total_playlist_appearances', 'total_chart_appearances']].sum().reset_index()
artist_analysis = artist_analysis.sort_values(by=['total_playlist_appearances', 'total_chart_appearances'], ascending=False)

#Display the top 10 artists

top_10_artists = artist_analysis.head(10)

#Plotting the bar graph for streams and playlist appearances of top artists

plt.figure(figsize=(12, 6))
plt.bar(top_10_artists['artist(s)_name'], top_10_artists['total_playlist_appearances'], label='Playlist Appearances')
plt.title('Top 10 Artists by Playlist')
plt.ylabel('Total Appearances')
plt.xlabel('Artist')
plt.show()

#Plotting the bar graph for streams and chart appearances of top artists

plt.figure(figsize=(12, 6))
plt.bar(top_10_artists['artist(s)_name'], top_10_artists['total_chart_appearances'], label='Chart Appearances')
plt.title('Top 10 Artists by Chart Appearances')
plt.ylabel('Total Appearances')
plt.xlabel('Artist')
plt.show()
```

#### 
