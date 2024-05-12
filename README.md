


SOLUTION:




The objective of the assignment was to create a movie recommendation system based on 2 possible methods- 
1. Content based
2. Collaborative filtering based


There are 5 ipynb files attached in this repo. Breaking down each one:

movieratings.ipynb

This code uses content based recommendation system to predict suitable movies. The user has to input three genres that they would like to watch and using this data,
we predict movies to be recommended. 
The basic algorithm is that we first store the TFIDF vectors for all the movies for their corresponding genres,
then based on the user's desired genres, we obtain the cosine similarity with all the movies to find the 3 most suitable movies to show. 

An important feature incorporated in this is that it is possible that the user inputs genres which are not part of the dataset,
so using GloVe embeddings we obtain genres similar to the genres given by the user which belong to the dataset and then proceed further with the cosine similarity. 
GloVe embeddings is a readymade model which captures the semantics between different words.

contentbased.ipynb

This is for the part 2 of the assignment which uses both ratings.csv and movies.csv.

This code also uses content based recommendation system but the underlying algorithm is different for this case.

After receiving the userID from the user, we suggest recommended movies to watch based on the 10 recent movies which the user has watched. 
We obtain the 10 recent movies watched by the user using the ratings.csv dataset by arranging it with respect to the timestamp column.
This is followed by obtaining the genres for each of those 10 recent movies and getting the 5 most watched genres using the movies.csv dataset.
After we find the 5 most recently watched genres, using TFIDF vectorization, we obtain the cosine similarities of those 5 genres with all the movies in the dataset to 
predict the 10 most suitable movies to watch for the user based on their recent watching history. 

This algorithm uses recent watching history to determine suitable movies.

anothercontentbased.ipynb

This code is again for the part 2 of the assignment which uses both ratings.csv and movies.csv but uses a different algorithm than the one before
to recommend movies based on the content based recommendation system.

After receiving the userID, we sort the movies rated by the user based on the ratings.csv dataset in the descending order of the ratings and selects the 10 most highly rated movies based on the ratings as well as the timestamp such that the movies selected are the most recently highly rated movies by the user. 
After getting the 10 movies, we obtain their corresponding genres based on the movies.csv dataset and select he 5 most repeating genres in those movies.
After getting the 5 genres, the procedure is the same as the previous algorithm. We apply TFIDF vectorization to all the movies in the dataset as well as 
the user based genre array and then select the 10 movies with the highest cosine similarity.

This algorithm uses rating history to predict suitable movies.


collaborativesystembased.ipynb

This code is for the second part of the part 2 of the assignment as well as for the second part of the part 1 of the assignment.

Collaborative recommendation systems predict the preferences or ratings that a user would give to a particular item (e.g., a movie, a product) based on the preferences or ratings of similar users.

The underlying idea behind collaborative filtering is that users who have similar tastes or preferences in the past are likely to have similar tastes in the future. Therefore, the system can make predictions for a user by finding other users who are similar to them and aggregating their preferences.


So the underlying algorithm for this system is as follows.
First we reduce the dataset such that only the highly rated movies for each user remain ( above 4 ). After this is done, we further reduce the dataset by removing movies
which have number of ratings less than 0.01% of the total ratings given by all the users for all the movies. 
After this is done, we get a reduced number of movieIDs to work with. Then we use vectorization to create a vector for each user based on the movies watched by them
and the corresponding ratings given. Here, we have set the vector such that value 2 is given to the movie column of all users for which the user has given 5 as the rating.
1 is given to movies with ratings 4 or 4.5 and 0 for the other movie columns.
After this, we input the userID for which movies are to be recommended. After receiving the userID, we get the corresponding vector for the user and then we apply cosine 
similarity ( using SURPRISE LIBRARY ) with all the vectors to find the user who has the most similar taste. This is how collaborative filtering is done here.
Then after obtaining the most similar userID, we recommend movies which are watched and rated highly by the similar user but not by out desired user. If less than 10 movies are different between them, then we use the second most similar ser for recommending the remaining movies. 

Thus, this algorithm uses collaborative filtering system for recommending movies.

collaborativesystem.ipynb

This is a simpler collaborative filtering system based recommendation algorithm.

Using SUPRISE library, we use SVD matrix decomposition to understand the relationships between movie ratings of different users and then and then 
after inputting required userID, it predicts movie ratings and recommends top 10 rated movies.
This algorithm requires lot of computational time as the dataset is huge and SVD needs to compute 3 matrices of very high dimensionalities. 

