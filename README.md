
![alt text](/Image/alfredo.jpg)

Review is a critical success metric for a lot of Business espically in Restaurant business where it has the power to drive its fate . 

The Business team of a restaurant uses the reviews to gauge its performance and potential and on the other side of the table The Customers depend on the reviews, from deciding whether to visit a restaurant to what to expect .

There are a lot of amazing platforms which cater to this need , Zomato , Yelp ,Google etc. naming a few, which make it very easy for people to read and post reviews . Thus there are huge banks of reviews . 

But with heaps of reviews available it is impossible for people to read all the reviews . This is where Taste Bots comes into the picture.


Taste Bots uses Natural Language Processing techniques on the Restaurnt reviews and makes sense of them . The solutions are

1) <a name="top1">Highlights most talked about features with its associated sentiment of a Restaurant.</a>

![alt text](/Image/blog1.png)
![alt text](/Image/blog3.png)

2) <a name="top2">Give reccomendations based on the reviews.</a>

![alt text](/Image/blog2.png)

### The process involves -:
1. Getting the data
2. Preprocessing the date which involves -:
      - Data cleaning.
      - Using symspell to correct spelling mistakes.
      - Lemmatization
3. [Learning most talked about features of a Restaurant and their sentiments .](#top1)  
4. [Topic modelling (For the recommended system)](#top2)


### Getting the data
The dataset used was <a href="https://www.kaggle.com/himanshupoddar/zomato-bangalore-restaurants">Zomato Bangalore Restaurants</a> .
Our main interest in the dataset were the  name,review_list and rating.

### Preprocessing
#### Data Cleaning

1. From the dataset few restaurant which had sufficient reviews were picked .
2. The columns name and review_list were selected .
3. The review from review list were cleaned using regex and other techniques .
4. Finally the cleaned dataset was saved to <a name='rest_excel' href="https://github.com/codedribbler/Taste-Bots/blob/master/Code/Restaurant_Review.xlsx">Restaurant Review</a> excel file .


#### Symspell
Spelling error is omnipresent in reviews . So before further working in reviews it is important to first mitigate the mispellings as much as possible .
To correct spellings a library called <a href="https://github.com/wolfgarbe/SymSpell">Symspell</a> is used. We have extended its functionality by including indian food and dish names in its dictionary so that it serves our purpose .

#### Lemmatization
Lemmatization involves resolving words to their dictionary form. In fact, a lemma of a word is its dictionary or canonical form. So words like loved, loving etc. will have thier lemmatized form as love.

[The Restaurant Review excel](#rest_excel) contains the output after each review of restaurant is sanitized by passed it through symspell followed by lemmatization function. 


### Learning most talked about features of a Restaurant and their sentiments

One of the objecive of the project is to highlight the most noticed feature of a restaurant .
Explain by example ...........



So in the file [The Restaurant Review excel](#rest_excel) we have data consisting of different restaurants and thier reviews . So for each restaurant, reviews would be picked and following tasks would be performed on them -:

**1. Splitting the reviews in sentences** - The reviews will be divided into sentences. This can just be done by splitting the reviews based on punctuations('.',','etc.) but punctuation mistakes are quiet common in reviews, so a library <a href="https://github.com/notAI-tech/deepsegment">DeepSegment</a> is used . DeepSegment has nice performance in Sentence segmentation or Sentence boundary Detection and it outperforms both Spacy and NLTK in this task .

**2. Feature Extraction** - Spacy is used for Feature Extraction . After a review is segmented, each sentence is parsed with spacy and using noun_chunks functionality of spacy the features are extracted, then if noun_chunks contains stop words like the,a etc. and this cycle goes for all the sentence of the review . In this way features mentioned in a particular review are collected . Then using a counter occurances of the features in the list would be counted . Features which are less than 0.05 times number of reviews will be dropped. In this way only frequently mentioned features are considered.

All the reviews of a particular restaurant goes through the same process and the final feature list consists of all the features mentioned in reviews and using this process features of all the restaurant is collected in a dictionary.


**4. Extracting Sentiments and Sentiment Score** - To find setiment of features, reviews of a restaurant will be iterated to find if the contain the feature mentioned corresponding to that restaurant in feature dictionary. If the feature is located in the review, using spacy dependency parsing, adjective which describes the feature is be searched around the feature. So a dictionary is created with features as its key and the adjective as its values .

After the dictionary is created, the values of the dictionary i.e the adjectives are converted into sentiment score using AFINN .  The <a href="https://pypi.org/project/afinn/">AFINN</a> lexicon is perhaps one of the simplest and most popular lexicons that
can be used extensively for sentiment analysis.

This is done for all the restaurant and the final sentiments are saved in <a href="https://github.com/codedribbler/Taste-Bots/blob/master/Code/sentiment_matrix.xlsx">Setiment Dataset</a>.




