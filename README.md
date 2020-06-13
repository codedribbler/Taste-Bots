# Taste-Bots

Inline-style: 
![alt text](/Image/Rest1.jpg)

Folder : Code
	
	a) DataMine.ipynb - This files gets the data from the main zomato.csv file, cleans the reviews of the restaurants which were demonstrated in the project then outputs the reviews with restaurant name in Restaurant_Review.xlsx file.
	
	b) Sym spell and lemmatize.ipynb - Takes the restaurant reviews from Restaurant_Review.xlsx and after processing the reviews gives the corrected output back to Restaurant_Review.xlsx
	
	c) Feature Extraction and Sentiment.ipynb - Takes the restaurant names and reviews from Restaurant_Review.xlsx and give outputs in \Flask\sentiment_matrix.xlsx.
	
	d) Data Cleaning topic modelling.ipynb -- this is used to clean the data for topic modelling, it will use zomato data file.

	e) Topic Modelling Final.ipynb -- Topic modelling is done on the cleaned dataset to get the distribution score for each restaurant and clustering is performed on the distribution scores to get the similar clusters

  
  
Files used by symspell
	a) frequency_bigramdictionary_en_243_342
	b) frequency_dictionary_en_82_765
	c) slang
	d) StopWords_Generic
  
The dataset used for zomato bangalore restaurant dataset taken from kaggle 
  link :-https://www.kaggle.com/himanshupoddar/zomato-bangalore-restaurants/download/qN48oJNnMh4H98ZK18NW%2Fversions%2FtLWHPyi9rFWVzhJ57UZ3%2Ffiles%2Fzomato.csv?datasetVersionNumber=1

