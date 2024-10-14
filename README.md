# Spotify genre predictiion in R
### Goal

Analysing and building predictive models
for Spotify to predict the genre of the song by using data such as

      - the year the song was released
      - how “speechy” the song is
      - how danceable the song is
      - the tempo of the song

### Steps followed 

- Step 1 : Loading the necessary libraries such as Tidyverse,ggplot, lubridate and tidymodels
- Step 2 : Reading the .csv file dataset which is at a remote location to a dataframe.
- Step 3 : Skim without charts gives vital information such as number of rows and columns in the dataset and differentiate charcter and numeric variables.
![skimr](https://github.com/user-attachments/assets/41ed2b6a-3c57-44cb-a37a-b13f725e57e7)
- Step 4 : Getting rid of null values by 
            
            spotify_songs <- na.omit(spotify_songs)

- Step 5 : Slicing the dataset to 1000 songs in each genre. Using the pipe operator '%>%' from dpylr in R , you can basically recreate SQL syntax in R. 
            
            song_select <- song_select %>%
            group_by(playlist_genre) %>%
            sample_n(1000) %>%
            ungroup()

- Step 6 : Factorizing the target variable by using as.factor, R automatically converts it for you.
            
            song_select$playlist_genre = as.factor(song_select$playlist_genre)

- Step 7 : To get insight into the data, visualization is done. Plotting a side by side boxplot of Popularity vs Genre helps in gaining valueble insights.
![pvsg](https://github.com/user-attachments/assets/5c685b2c-8df0-4ef6-952b-f232e554208f)

            a) It is evident that ‘Pop’ has the most poluarity
            b) ‘Latin’ slightly less popular than pop
            c) Rest of the genre having relatively high popularity than ‘EDM’
            d) Popularity differs between genres

- Step 8 : Next step is to plot a side by side boxplot on Speachiness vs Genre.
![speachvsgenre](https://github.com/user-attachments/assets/496485d9-3845-4a40-9088-90410af8c4cf)

            a)The above box plot concludes that ‘Rap’ and ‘R&B’ genre has more speechiness distribution.
            b)‘Rock’ genre being the least.
- Step 9 : Next step is to visualise the mean popularity of a genre over the years from 1960 to 2020.
![avg](https://github.com/user-attachments/assets/6a8738c4-c998-4a02-a077-94247b63082a)

- Step 10 : Splitting the training and test data in the rato of 80:20. Random state is introduced so that if you run a different instance to get the same data to be split you shoudl use the same state. 

- Step 10 : First model to build is  Linear discriminant analysis (LDA).

      set.seed(1893161)
      song_split = initial_split(song_select)
      song_train = training(song_split)
      song_test = testing(song_split)

## Evaluation of model

Evaluation of linear regression is as follows

![accuracy](https://github.com/user-attachments/assets/45cb1650-795e-4ab5-9197-1145c7b50d6b)

Following inferences can be drawn from the output

##### [1] Accuracy of only 0.408 is achieved with LDA.
##### [2] Future work is required using KNN and Random forest regression.
