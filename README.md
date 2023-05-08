# MusicRecommenderCF
 Music recommender system based on collaborative filtering using the ListenBrainz listens dataset.
 
 ## Summary
This project aims to develop a music recommendation system using collaborative filtering with the ListenBrainz database. The goal is to create a model that can recommend artists to users based on their listening history, by identifying patterns in the listening behavior of similar users.

The project consists of two main parts divided in two different Colab Python Notebooks: data processing (`ListeningBrainzColFilt_DataTransform.ipynb`) and model generation (`ListeningBrainzColFilt_RecomModel.ipynb`).

In the data processing step, the files containing the listening history of the users from the ListenBrainz database are parsed and transformed into a final csv file containing the id of each user, an id for each artist and the playcount of each artist by that user. 

This file is then used in the model generation step, where a sparse matrix is created from the user and artist indexes, and the nearest neighbor's similarity is computed using alternating least squares. The model's accuracy is evaluated by testing it on a set of artists and comparing its recommendations to those of other recommender systems.

Technologies used in this project include Python, Pandas, NumPy, and the implicit library for collaborative filtering.

## Data
The ListenBrainz data is distributed in 12 files, one for each month of 2022.

Every listen is identified by a `recording_msid` that is random (the same song could have multiple different `recording_msid`). To compare the data we need to convert this id into a `recording_mbid` that is present in the database.

To do this there are three additional files:
- A mapping between each `recording_msid` and `recording_mbid` in the  ListenBrainz database (`listenbrainz_msid_mapping.csv`)
- The ListenBrainz Canonical Metadata database, which includes a list of all `artist_mbid` (`canonical_musicbrainz_data.csv`).
- `artist_mbid` to artist name mapping, with the name of all artists in the MusicBrainz database. (`musicbrainz_artist_mbid_name.csv`)

## Model
The model uses a collaborative filtering recommendation system to make personalized recommendations by analyzing user-artist interactions. Data is stored in a sparse matrix, weighted using the BM25 algorithm, and the Alternating Least Squares (ALS) algorithm is used to learn the latent features of the users and artists. The model finds the most similar items using cosine similarity and provides a list of recommended items sorted by their similarity score.

## Results
To evaluate the model's accuracy, it's tested for some known artists and check the resulting recommendations.

Artist recommendations for _Iron & Wine_
|n|score	 | artist_name |
|:---: | :---:    | :---:     |
|0|	1.000000 |	Iron & Wine |
|1|	0.422283 |	Gregory Alan Isakov |
|2|	0.390881 |	Fleet Foxes |
|3|	0.383695 |	The Shins |
|4|	0.376312 |	Bon Iver |
|5|	0.375864 |	José González |
|6|	0.369226 |	Sufjan Stevens |
|7|	0.365435 |	Lord Huron |
|8|	0.360813 |	Death Cab for Cutie |
|9|	0.341159 |	The Head and the Heart |

Artist recommendations for _Masayoshi Takanaka (高中正義)_
|n|score|artist_name|
|:---:|:---:|:---:|
|0	|1.000000|	高中正義|
|1	|0.386140|	Casiopea|
|2	|0.328007|	大貫妙子|
|3	|0.326699|	T‐SQUARE|
|4	|0.301526|	杏里|
|5	|0.278965|	Lamp|
|6	|0.277665|	Naniwa Express|
|7	|0.277088|	Piper|
|8	|0.269268|	Serge Ponsar|
|9	|0.268987|	TUCKER|

Artist recommendations for _The Band_
|n|score|artist_name|
|:--:|:---:|:---:|
|0	|1.000000|	The Band|
|1	|0.518695|	Van Morrison|
|2	|0.494562|	Crosby|
|3	|0.464024|	Bob Dylan|
|4	|0.462077|	Crosby|
|5	|0.435122|	Grateful Dead|
|6	|0.425560|	George Harrison|
|7	|0.420686|	Neil Young|
|8	|0.418821|	The Byrds|
|9	|0.413197|	Warren Zevon|
