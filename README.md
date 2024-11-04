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
import pandas as pd
import matplotlib.pyplot as plt
```

#### The pandas library is an easy-to-use data structure and data analysis tool for manipulating and analyzing structured data, while the Matplotlib library is used for data visualization. Both of these libraries are the key tools to accomplish this activity.

#### Using the downloaded `.csv` file containing the "Most Streamed Spotify Songs 2023", we will load the file into 'spotify_data'.
```python
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
pd.set_option('display.max_columns', None)
```

#### To revert back to the original pandas display settings, this code is to be used:
```python
pd.reset_option('All')
```

---

## **Overview of the Dataset**

#### We can begin the exploratory data analysis now that we can see our dataset.

#### The size or dimension of our dataset can be known using the `.shape` attribute.
```python
print("Number of rows and columns:", spotify_data.shape)
```
>Output:

![image](https://github.com/user-attachments/assets/320aba75-802a-474a-ab38-89da8092d656)

#### The dataset has **953 rows** and **24 columns**.

#### Now, let's get the information of our dataset. We will use the `.info()` attribute to identify the data types of each column of the dataset.

```python
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

## **Basic Descriptive Statistics**

#### In this section, we will explore basic descriptive statistics of the streams of the songs in the dataset by calculating its mean, median, and standard deviation to understand the average number of streams, the middle ground of streams, and the variation in streaming activity. These statistics will provide a better understanding of the dataset.

### **Mean**

#### Going back to the overview of the dataset, we discovered that the streams column is an object but we need it to be in numerical value so that we can calculate its mean.

#### Let's convert the datatype of the streams column:
```python
streams = spotify_data['streams'].astype(float)
```
>Output: 

![image](https://github.com/user-attachments/assets/e566f087-6223-45d6-a28c-3ec7b7999cdc)

#### We can now calculate the mean of the streams column using the `.mean()` attribute and `round` function to make our mean in two decimal places.
```python
mean_streams = round(streams.mean(), 2)
mean_streams
```
>Output:
![image](https://github.com/user-attachments/assets/bcda3e1d-bd8e-4867-96cd-a8398c67e51d)

#### The average stream value of the "Most Streamed Spotify Songs 2023" dataset is 514,137,424.94.

### **Median**

#### We can get the median of the streams column by using the `.median()` attribute:
```python
median_streams = streams.median()
median_streams
```

>Output:
![image](https://github.com/user-attachments/assets/24c7dca1-8a88-4ebf-ac89-f3b7ec83937e)

#### The median value of the streams in the "Most Streamed Spotify Songs 2023" dataset is 290,530,915.


### **Standard Deviation**

#### We will use the `.std()` attribute to compute the standard deviation of the streams column and `round()` function to make our result in two decimal places:
```python
std_streams = round(streams.std(),2)
std_streams
```

>Output:
![image](https://github.com/user-attachments/assets/3d616347-15d6-40f9-9dc4-2f40270e5c7b)

#### The standard deviation of the streams of the "Most Streamed Spotify Songs 2023" dataset is 566,856,949.04. 

#### We can notice that the standard deviation value is higher than the mean. This tells us that the range of stream data varies greatly indicating that some songs are significantly more popular than others.

### **Distribution**

---

## **Top Performers**

#### In this section, we will identify the top streamed tracks and most frequent artists from the "Most Streamed Spotify Songs 2023" dataset.


### Top 5 Most Streamed Track

#### To identify the top streamed tracks of the dataset we will use `.sort_values(by = 'streams', ascending = False]` attribute to sort the tracks by number of streams in descending order and `.head()` function to display the top 5 of the list.
```python
sorted_stream = spotify_data.sort_values(by = 'streams', ascending = False)
sorted_stream.head()
```

>Output:
![image](https://github.com/user-attachments/assets/1542e872-3735-414e-82d2-380cb7a54410)

#### The most streamed track in Spotify during 2023 is **Blinding Lights** by The Weeknd with 3,703,895,074 streams.

### Top Artists

#### To count the frequency of each artists in the dataset, the `.valuecounts()` function and the `.head()` is used to display the top 5 most frequent artists.
```python
artist_count = spotify_data['artist(s)_name'].value_counts()
artist_counts.head()
```

>Output:
![image](https://github.com/user-attachments/assets/d6872024-8586-41d2-872f-0b1142dbd6d4)

#### Here we can see that that the top five most frequent artists are Taylor Swift with 34 songs, The Weeknd with 22 songs, Bad Bunny with 19 songs, Sza with also 19 songs, and Harry Styles with 17 songs.

---

## Temporal Trends

#### In this section, we will analyze the trends in the number of tracks based on its year of release and month of release. Observation on the visualization that will be produced will help generate insights and ideas id and how time contributes to the number of streams of Spotify songs during 2023.

### Tracks and Released Year

#### To organize the tracks in the dataset to its year of release we will use the `.sort_index()` attribute to sort by labels along the x-axis.

#### The graphical representation to be used for data visualization is the bar graph. The visualization can be achieved with the Matplotlib library using the following:
#### `plt.figure(figsize=( , ))` for the figure size
#### `plt.title` for the graph title
#### `plt.xlabel() for the label on x-axis
#### `plt.ylabel() for the label on y-axis
#### `plt.grid(axis='y')` to generate the gridlines for better viewing
#### `plt.show()` to display the graph
```python
tracks_year = spotify_data['released_year'].value_counts().sort_index()
plt.figure(figsize=(15, 8))
tracks_per_year.plot(kind='bar')
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

### Tracks and Released Month

#### To organize the tracks in the dataset to its month of release we will use the `.sort_index()` attribute to sort by labels along the x-axis.

#### The graphical representation to be used for data visualization is the bar graph. The visualization can be achieved with the same method from the *No. of Tracks Released Per Year* graph.
```python
tracks_month = spotify_data['released_month'].value_counts().sort_index()
plt.figure(figsize=(15, 8))
tracks_per_month.plot(kind='bar')
plt.title('No. of Tracks Released Per Month')
plt.xlabel('Year')
plt.ylabel('No. of Tracks Released')
plt.grid(axis='y')
plt.show()
```

>Output:
![image](https://github.com/user-attachments/assets/51ebdc26-df27-49cf-b68e-39a2c5e3f7c9)

