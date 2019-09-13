# Project Description
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.

## Sparkify would like a Data Engineer to create an Apache Cassandra database with tables designed to optimize queries on song play analysis.

# Data
the information we have is as follows:
  - artist
  - firstName of user
  - gender of user
  - item number in session
  - last name of user
  - length of the song
  - level (paid or free song)
  - location of the user
  - sessionId
  - song title
  - userId
### The image below is a screenshot of the denormalized data
![alt text](https://github.com/Katba-Caroline/Data_Modelling_Cassandra/blob/master/Cassandra.jpg)


# Queries
## Sparkify wanted answers to these three questions, therefore we had to create tables specifically optimized for these queries. 
    
    1. Give me the artist, song title and song's length in the music app history
    that was heard during sessionId = 338, and itemInSession = 4
    
    
    2. Give me only the following: name of artist, song (sorted by itemInSession)
    and user (first and last name) for userid = 10, sessionid = 182
    
    
    3. Give me every user name (first and last) in my music app history
    who listened to the song 'All Hands Against His Own'
    
    
## Query 1
  **Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4**
  - *Table name*: tracks_per_session
  -  *Columns* : sessionId, itemInSession, artist, song_title and song_length.
  - *Primary Key* : Partition Key "sessionId" and clustering key "itemInSession"
  - *CQL Query*: 
         
         SELECT artist, song_title, song_length 
         FROM tracks_per_session
         WHERE sessionId = 338 AND itemInSession = 4

## Query 2
  **Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182**
  - *Table name*: user_playlist
  -  *Columns* : userId, sessionId, itemInSession, artist, song, firstName and lastName.
  - *Primary Key* : Partition Key is composite of "userId" & "sessionId" and clustering key "itemInSession"
  - *CQL Query*: 
         
         SELECT itemInSession, artist, song, firstName, lastName
         FROM user_playlist
         WHERE userId = 10 AND sessionId = 182
         
         
## Query 3
  ** Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'**
  - *Table name*: user_history
  -  *Columns* : song, firstName, lastName and userId.
  - *Primary Key* : Partition Key "song" and clustering key "userId"
  - *CQL Query*: 
         
         SELECT firstName, lastName 
         FROM app_history 
         WHERE song = 'All Hands Against His Own'
