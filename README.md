
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
3. [Finding the most talked about features of a Restaurant and their sentiments .](#top1)  
4. [Topic modelling (For the recommended system)](#top2)


### Getting the data
The dataset used was <a href="https://www.kaggle.com/himanshupoddar/zomato-bangalore-restaurants">Zomato Bangalore Restaurants</a> .
Our main interest in the dataset were the  name,review_list and rating.

### Preprocessing
#### Data Cleaning

1. From the dataset few restaurant which had sufficient reviews were picked .
2. The columns name and review_list were selected .
3. The review from review list were cleaned using regex and other techniques .
4. Finally the cleaned dataset was saved to an <a href="https://github.com/codedribbler/Taste-Bots/blob/master/Code/Restaurant_Review.xlsx">Restaurant Review</a>. 




