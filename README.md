# Spotify-Genres-Classifying-Genre-by-Audio-Features-and-Lyrics
Author: Sean Reidy

UMBC DATA 601 Fall 2020

Final Project

![spotify_genre](https://community.spotify.com/t5/image/serverpage/image-id/27674iC82331350312CE8A/image-size/original?v=mpbl-1&px=-1)

This project is an utilizes the [Spotify Web API](https://developer.spotify.com/documentation/web-api/) in conjunction with the [Genius Web API](https://genius.com/developers). exploring, analysing, modeling genre by using  different audio features from 13 different Spotify genres.

The report and modeling can be found in [Report.ipynb](https://github.com/sreidy/Spotify-Genres-Classifying-Genre-by-Audio-Features-and-Lyrics/blob/master/Notebooks/Report.ipynb)

The final model is a Random Forest Classifier, with 70% accuracy at predicting genre.

# Goals

It is obvious to most individuals what a musical genre sounds like, it's quite easy to say one song is rock and another is rap after only to listing for a few seconds. What’s difficult is asking why? Why is song X rock and not rap?  What natural heuristics did we use in our heads to make this decision? For Music, and other creative media,  there are no predefined rules for classifying a track or artists with a genre. With this project I hope to define genre in more quantitative factors,  such as a song's popularity, the key, and other audio features. 

 - What characteristics objectivly define a music genre? 
  - Is it possible to classify traks into a genre from audio feautres and lyric data? 
  - Are some genres more diverse than others? And how so,  is the genre creatively contraited by the trappings of the genre? 
 - What is better at defining genre, is it the audio features (such as tone, valance, or danceability) or is the lyrical content of a song more effective for a classification model?
 - Does incorpering NLP features on lyrical content help improve classification of genre? 
 - How does lyrical sentiment, and profanity differ across genre? 
 - Does there exist a relationship between the Valence (musical tone of a song: happy or sad) and Lyrics Sentiment (are the lyrics themselves happy or sad)? 
 - Using our understanding of genre from our models is it possible to generate music and lyrics of a given genre?

Looking at the technical and programming aspects of this project.  I wanted to learn and implement parallel processing for the data collection process. Earlier in this project I had realized that the volume of data I would need to pull from the Spotify API would be much greater than my past work. Pulling tracks one at a time would not be practical, so I wanted to learn how to parallelize this process with Pythons Concurrent Futures package. 

# Motivation & Background

If you're a Spotify user like myself, I’m almost certain you were fascinated by your recent spotify wrapped for 2020. Spotify’s yearly summary of your musical adventures on the platform, serving as an “best of” montage of your music. 
 

This year in particular given the circumstances of our new lives, many user's musical habits and even tastes have shifted and changed. Music is deeply personal and varied, as this year has made some of us branch out into new genres, and others look back at comfort songs from our youth. There is reason to suspect that these changes in taste is a response to stress and environmental factors. [More info on shifting tastes in music during the pandemic](https://www.vice.com/en/article/m7j8gq/pandemic-changing-music-taste-nostalgia) 

Similar projects and tutorials references on the Spotify Web API and python data science
- [Every Noise](http://everynoise.com/) an ongoing project mapping and cataloging every single spotify genre
- https://medium.com/@maxtingle/getting-started-with-spotifys-api-spotipy-197c3dc6353b Shows how to implment the Spotipy python package to acess the Spotify Web API and save the results to a pandas data frame.
- https://www.kaggle.com/nicapotato/top-spotify-tracks-2019-eda/execution An example of EDA on spotify feature data 
- https://www.kaggle.com/aniruddhachoudhury/classify-song-genres-from-audio-data-model Refrenced for testing and comparing moddle results 


# Table of Contents

- Data: Data is not included in this Github repo due to file size restrictions.To Download any of the data used follow this [google drive link](https://drive.google.com/drive/folders/1VDrB8YQwvpXE2hfbGoMrfkSLLyBG92R3?usp=sharing) 

- Notebooks
	+ [Report.ipynb](https://github.com/sreidy/Spotify-Genres-Classifying-Genre-by-Audio-Features-and-Lyrics/blob/master/Notebooks/Report.ipynb): Notebook containing the report and modeling  
	+ [GettingData.ipynb](https://github.com/sreidy/Spotify-Genres-Classifying-Genre-by-Audio-Features-and-Lyrics/blob/master/Notebooks/GettingData.ipynb): Pulling from both the Spotify Web API and the Genius Web API
	+ [EDA.ipynb](https://github.com/sreidy/Spotify-Genres-Classifying-Genre-by-Audio-Features-and-Lyrics/blob/master/Notebooks/EDA.ipynb): Exploritroty 
	+ [FeatureEngineering.ipynb]( https://github.com/sreidy/Spotify-Genres-Classifying-Genre-by-Audio-Features-and-Lyrics/blob/master/Notebooks/FeatureEngineering%20.ipynb): cleaning, and saving the data, removing outliers. 
	
# Software Requirements & Usage

- Packages Used: 
	+ [Spotipy](https://spotipy.readthedocs.io/en/latest/#): A Python library for the [Spotify Web API](https://developer.spotify.com/documentation/web-api/)
    + [lyricsgenius](https://pypi.org/project/lyricsgenius/) : A Python wrapper for the [Genius Web API](https://genius.com/developers)
	+ [getpass](https://pymotw.com/2/getpass/#module-getpass): A Python library to hide spotify web API credentials 
	+ [pickel](https://docs.python.org/3/library/pickle.html): used to save the spotify dataframe to disk
	+ [pandas](https://pandas.pydata.org/docs/)
	+ [matplotlib](https://matplotlib.org/3.3.3/contents.html)
	+ [seaborn](https://seaborn.pydata.org/)
	+ [scikit-learn](https://scikit-learn.org/stable/)
    + [re](https://docs.python.org/3/library/re.html) Regular expression operations 
    + [nltk](https://www.nltk.org/) Python Natural Language Toolkit 
    + [wordcloud](https://amueller.github.io/word_cloud/index.html) 

# Dataset

Illustrated in the image above is the process used to collect the data from both the Spotify Web API and the Genius API. Two different Python API wrappers were used to interact with the API’s, [Spotipy](https://spotipy.readthedocs.io/en/2.16.1/) and [lyricsgenius](https://pypi.org/project/lyricsgenius/) 

 There is a total of 6 root genres, each root genre has 5 of the most popular sub_genres, These genres were selected using the [Every Noise Project](http://everynoise.com/) By looking at the top most popular genres across all of Spotify, then selecting the associated sub genres. 
 - Pop : post teen pop, dance pop, electropop, pop dance, indie pop
 - Rap : hip hop. souther hip hop, gangster rap, trap, dirty south rap
 - EDM : electro house, big room, pop edm, pop dance, complextro
 - R&B : urban contemporary, new jack swing, neo soul, hip pop,pop r&b
 - Country : Country road, contemporary county, moden country rock, country rock, country dawn
 - Rock : album rock, classic rock, permanet wave, hard rock, modern rock

The Features of the Dataset
- track_id : a spotify primary key; unique for each track
- artist: name of artist
- album: name of album
- trackName: title of track
- root genre: (TARGET VAR) the root genre of the track, pop, rap, edm, R&B, Country, Rock
- sub genre: The associated sub genre of the track 
- acousticness: A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic.
- danceability: Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable. 
- duration_ms: The duration of the track in milliseconds.
- energy: a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. 
- instrumentalness: Predicts whether a track contains no vocals. “Ooh” and “aah” sounds are treated as instrumental in this context.
- key: The estimated overall key of the track. Integers map to pitches using standard [Pitch Class notation](https://en.wikipedia.org/wiki/Pitch_class) 
- liveness: Detects the presence of an audience in the recording.
- loudness: The overall loudness of a track in decibels (dB). 
- mode: indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. Major is represented by 1 and minor is 0.
- speechiness: Speechiness detects the presence of spoken words in a track.
- tempo: BPM of track
- time_signature: An estimated overall time signature of a track. 
- valence: A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. 
- category_id: The Spotify Category ID of the track 
- popularity: The value will be between 0 and 100, with 100 being the most popular. The artist’s popularity is calculated from the popularity of all the artist’s tracks.
- lyrics: A large string of song raw lyrics from the genius API
- lyrics_vector: lyrics, cleaned of new line chars and vectorized into a list 
- pos_tagging:  a list of tuples generated from nltk.pos_tag, Part of Speach 
- nouns: A total count of nouns in a track 
- verbs: a total count of verbs in a track
- adverbs: a total count of adverbs in a track 
- adjectives: a total count of adjectives in a track
- foreign_count: a total count of foreign(non english) words in a track 
- profanity_count: a total count of profanity in a track 
- lyrics_lemm: lyrics vectors that have been stemmed and lemmitized 
- lyrics_sentiment: The mean sentiment from nltk.sentiment.vader across all lines in the track lyrics. negative values is more sad,mean and postive values happy and upbeat. 


The Spotify Web Api provided the following Audio Features for each track [more info here](https://developer.spotify.com/documentation/web-api/reference/tracks/get-audio-features/)


