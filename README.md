# Project: Data Modeling with Apache Cassandra

## Project description

The goal is to create an Apache Cassandra database which models songs and user activity of a music streaming app.

## Project workspace

The project workspace consists of : 

 1. *Project_1B_ Project_Template.ipynb* : the notebook where all the process of collecting, transforming and quering data is described.
 2. */event_data* : data directory
 3. *README.md* : README file
 4. *event_datafile_new.csv* : CSV file which is created when data present in /even_data repository is denormalized. 

## Queries

<b>Query 1:</b>  Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4

```sql
select artist_name, song_title, song_length from music_history WHERE session_id = 338 and item_in_session 
```
<b>Query 2:</b> Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182

```sql
select artist_name, song_title, user_firstname, user_lastname from music_session WHERE user_id = 10 and session_id = 182"
```
<b>Query 3:</b> Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'

```sql
select user_firstname, user_lastname from music_usage WHERE song_title='All Hands Against His Own'"
```

## Database schema

In order to answer questions, I have created 3 tables:

	
	*music_history(artist_name, song_title, song_length, session_id, item_in_session)*

	*music_session(artist_name, song_title, user_firstname, user_lastname, user_id,session_id, item_in_session)*

	*music_usage(user_firstname, user_lastname, song_title)*

## ETL pipeline

All the process is described in the notebook *Project_1B_ Project_Template.ipynb*

 1. First, all the data from event_data is denormalized and gathered in event_datafile_new.csv

 2. Then, we create a Keyspace called *events* (Apache Cassandra should be installed localy) and tables : music_history, music_session, music_usage.

 3. Finally, we insert data from event_datafile_new.csv into the 3 tables and query them.




