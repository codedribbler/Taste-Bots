
![alt text](/Image/alfredo.jpg)

Customer reviews are a critical success metric for a lot of businesses espically in restaurant business where it has the power to drive its fate . 

The business team of a restaurant uses the reviews to gauge performance and potential and on the other side of the table the customers depend on the reviews, from deciding whether to visit a restaurant to what to expect .

There are a lot of amazing platforms which cater to this need Zomato , Yelp ,Google etc. naming a few, which make it very easy for people to read and post reviews . Thus there are huge banks of reviews . 

But with heaps of reviews available it is impossible for people to read all the reviews. This is where Taste Bots comes into the picture.Taste Bots uses Natural Language Processing techniques on the Restaurnt reviews and makes sense of them . 

The solutions Taste Bots provide are -:

1) <a name="top1">Highlights most talked about features of a Restaurant with its associated sentiment.</a>

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
The dataset used is <a href="https://www.kaggle.com/himanshupoddar/zomato-bangalore-restaurants">Zomato Bangalore Restaurants</a> .
Columns name,review_list and rating is used for the project.

### Preprocessing
**1.Data Cleaning**
1. From the dataset few restaurants which has sufficient reviews are picked .
2. The columns name and review_list are selected .
3. The reviews from review list are cleaned using regex and other techniques .
4. Finally the cleaned dataset is saved to <a name='rest_excel' href="https://github.com/codedribbler/Taste-Bots/blob/master/Code/Restaurant_Review.xlsx">Restaurant Review</a> excel file .


**2. Symspell**
Spelling error is omnipresent in reviews . So before further working in reviews it is important to first mitigate the mispellings as much as possible .
To correct spellings a library called <a href="https://github.com/wolfgarbe/SymSpell">Symspell</a> is used. Names of indian foods and dishes are appended in its dictionary so that it serves the purpose of the project.

**3.Lemmatization**
Lemmatization involves resolving words to their dictionary form. In fact, a lemma of a word is its dictionary or canonical form. So words like loved, loving etc. will have thier lemmatized form as love. The reviews are lemmatized using NLTK WordNet Lemmatizer.

[The Restaurant Review excel](#rest_excel) contains the output after each review of restaurant is sanitized by passed it through symspell followed by lemmatization function. 


### Learning most talked about features of a Restaurant and their sentiments

In a restaurant there can be features that customers mention in reviews . For example , suppose a restaurant serves scrumptious biryani and people really like it . So this would reflect in their reviews . So some reviews would be like -:

1) They have one of the best chicken biryanis in bangaluru.
2) Loved the Biryani.

and similarly if people would find thing like service, ambience , pizzas etc good or bad they would have their opinions on those .

One of the objective of the project is to draw out the features as well as thier opinions from the reviews and create a dashboard which will highlight the key things people are talking about a restaurant . This can have following utlity -:

1) **The owners of the Restaurant** can identify areas of improvement so that they can overcome the gaps and the areas which are doing well so that they canmarket them as their highlights in different channels.

2) **The customers** who very much likes to scrutinize the reviews of a restaurant before visiting, they will have a much more detailed analysis at their disposal.


The dataset [The Restaurant Review excel](#rest_excel) consists of different restaurants and reviews which were cleaned in preprocessing steps . For each restaurant, reviews are picked and following tasks are performed on them -:

**1. Splitting the reviews in sentences** - The reviews are divided into sentences. This can just be done by splitting the reviews based on punctuations('.',','etc.) but punctuation mistakes are quiet common in reviews, so a library <a href="https://github.com/notAI-tech/deepsegment">DeepSegment</a> is used . DeepSegment has nice performance in Sentence segmentation or Sentence boundary Detection and it outperforms both Spacy and NLTK in this task .

**2. Feature Extraction** - Spacy is used for Feature Extraction . After a review is segmented, each sentence is parsed with spacy and using noun_chunks functionality of spacy the features are extracted, then if noun_chunks contains stop words like the,a etc. they are removed and this cycle goes for all the sentence of the review . In this way features mentioned in a particular review are collected .This is repeated for all the reviews of a restaurant a collected in a list . Then using a counter occurances of the features in the list are counted . Features which are less than 0.05 times the number of reviews will be dropped. In this way only frequently mentioned features are considered.

All the reviews of a particular restaurant goes through the same process and the final feature list consists of all the features mentioned in reviews and using this process features of all the restaurant is collected in a dictionary.


**4. Extracting Sentiments and Sentiment Score** - To find setiment of features, reviews of a restaurant will be iterated to find if the contain the feature mentioned corresponding to that restaurant in feature dictionary. If the feature is located in the review, using spacy dependency parsing, adjective which describes the feature is be searched around the feature. So a dictionary is created with features as its key and the adjective as its values .

After the dictionary is created, the values of the dictionary i.e the adjectives are converted into sentiment score using AFINN .  The <a href="https://pypi.org/project/afinn/">AFINN</a> lexicon is perhaps one of the simplest and most popular lexicons that
can be used extensively for sentiment analysis.

This is done for all the restaurant and the final sentiments are saved in <a href="https://github.com/codedribbler/Taste-Bots/blob/master/Code/sentiment_matrix.xlsx">Setiment Dataset</a> and this dataset is used to create [UI](#top1) which provide dashboard for restaurants.



### Topic Modelling

<a href="https://en.wikipedia.org/wiki/Topic_model#:~:text=In%20machine%20learning%20and%20natural,structures%20in%20a%20text%20body.">Topic Modeling</a> is the process of identifying topics in a set of documents . In case of reviews topic modelling can be a handy utility which can find out around what topics the reviews are written . This can be leveraged to form recommended system which can -:

a. [Give recommendation of Restaurants based on the Topics](#top2)
b. [Give recommendation of restaurants similar ro a particular restaurant](#top2) 

There are other utilities as well which are not part of the project, like -:

a. Visually show to a restaurant owner what topics their positive and negative
reviews reside in. This makes it clear if a restaurant needs to improve its service
quality, or if its much more popular for its pizza than its bar.

b. Take a mean of all the restaurants and create an \average restaurant" in par-
ticular city or area. This will allow comparison of any restaurant against this
calculated mean.


The process for topic modelling is as follows -:


**1. Get the data** - Same <a href="https://www.kaggle.com/himanshupoddar/zomato-bangalore-restaurants">Zomato Bangalore Restaurants</a> dataset is required . Fileter the reviews whose ratings are greater than 3 . Then clean the reviews using same process as in the previous section.

**2. Tokenization** - Tokenization is a way of separating a piece of text into smaller units called tokens. Here, tokens can be either words, characters, or subwords. Here sentences are tokenized into words . Tokenization will create a list of words for each review . This way a 2d matrix is created where the row are the reviews and columns are the tokezed words . 

**3. Topic Modelling** - Two very popular approaches for topic modelling is used 
a. <a href="https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation">Latent Dirichlet allocation(LDA)</a> . <a href="https://radimrehurek.com/gensim/">Gensim</a> library ca be leveraged for doing LDA .  
b. <a href="https://en.wikipedia.org/wiki/Non-negative_matrix_factorization">Non-negative matrix factorization(NMF)</a> . It can be done using <a href="https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.NMF.html">sklearns NMF</a> 

NMF gave more interpretable results and separable topics.
--Photo of topcs

The topics can be categorized as -:
a. Biryani/order
b. Mutton Biryani
c. Ambience
d. Service/Staff
e. Buffet

Each review will have the topic distribution which will indicate how much the review is inclined to topics, this will help to identify the topic to which a particular review is annotating to .

For a restaurant the topic distribution of its reviews is averaged . This results in a vector which indicates the topic distribution of the restaurants .

These topic distribution vectors are leveraged to create recommendation system . The recommendation system cuurently can do the following things -:

1) Can give recommendation for restaurants known for **biryani, ambience or service** . For biryani the restaurants vector are sorted in descending order based on biryani score . Higher score restaurant will be recommended more . Similar process is followed fo ambience and service.

2) Can give recommendation of **similar restaurants** based on the selected restaurant . For doing this, cosine similarity of the restaurant vectors is calculated with the selected restaurants vector and the scores are sorted in descending order . Higher similarity scores will be recommended more.







