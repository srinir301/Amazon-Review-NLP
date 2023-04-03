# Amazon-Review-Sentiment-Analysis

![a_generic_white_10_us_noto_email_v2016_us-main _CB627448186_](https://user-images.githubusercontent.com/122238220/229404457-7180cf5e-19cf-4e2f-a0cc-6fbbed48bd8e.png)

## Business Understanding

My stakeholder is Amazon and other companies that sell their products on Amazon.com that want to improve their customer satifaction and future products overall. Having improved customer satisfaction then helps create improved brand loyalty which creates increased profits.

## Data Understanding

I got my data set from Amazon Web Services(AWS) and the I only got the wireless product reviews because that dataset already had over 8 million reviews. The data set included over 8 million rows and 15 columns including
- Marketplace
- Customer ID
- Review ID
- Product ID
- Product Parent
- Product Title
- Product Category
- Star Rating(**Target**)
- Helpful Votes
- Total Votes
- Vine
- Verified Purchase
- Review Headline
- Review Body(**Predictor**)
- Review Date

My project is predicting on the star rating which rates products from 1 to 5 stars and I am using the the review body text to predict on that. This is a multi class classification project, but the classes are condensed from 5 classes to 3 classes. The first class is 1 and 2 stars which are negative reviews, the second class is 3 stars which is the neutral reviews, and the third class is 4 and 5 stars which are the positive reviews.

## Preprocessing

I started out by dropping the null values which were in the review body, review headline, and review date columns. After dropping the null values I dropped unnecessary values which were not wireless values in the product category section because I only want to focus on the wireless products and some of the values were numeric. I saw there was a class imbalance in my data set which I originally tried to fix with SMOTE, but I ended up using random over sampler because SMOTE did not fix the class imbalance for me. I then sampled 10,000 reviews from the dataset because over 8 million reviews would have been too much.

## Preparation

To prepare my data for modeling I had to first use word tokenization to split up the sentences into words, then I lowercased all the words so that I can get rid of the stopwords in the my dataset and the make modleing less complex. I got rid of all the stop words to decrease the complexity of my models and I used Porter Stemmer to make the same type of words as one. Stemming decrease the complexity and I used it compared to other stemmers because it takes into account shorter words and it is a faster process. I decided not to use lemmatization because it would have taken longer to process, but it could have been more effective. Lastly I used TFIDF Vectorizer to take into account the importance of certain words and not just the count like using the Count Vectorizer.

**Class Imbalance**

![Count plot](https://user-images.githubusercontent.com/122238220/229406843-f33ee5ce-828a-4f9c-bf42-f91ee7ca6ed4.jpg)

## Modeling

I started out with a base logistic regression model with a precision of 79% which is a great start

**Base Logistic Regression**

![logreg best](https://user-images.githubusercontent.com/122238220/229406661-4c6e81ac-b6fb-44a1-b38e-3785beadbddd.jpg)

Then I created KNN, XGB, and Random Forest models with precision scores of 54%, 77%, and 72% respectively. These precision scores were not as good as the base logistic regression models. I used max depth, max leaves, and number of estimators to fix the class imbalance for the models. I used precision scores because I wanted a model that does well at predicting the actual classes.

**KNN**

![knn](https://user-images.githubusercontent.com/122238220/229407208-d5ea713f-585f-402f-8dcc-a2e8b2f4e687.jpg)

**XGB Classifier**

![xgbclass](https://user-images.githubusercontent.com/122238220/229407250-d7ac8b76-d463-4072-a289-9da4851c49da.jpg)

**Random Forest Classifier**

![rand forest](https://user-images.githubusercontent.com/122238220/229407302-346c84cd-2f2e-4d45-900d-83b15e118c96.jpg)

## Evaluation

I ended up using the base logistic regression model which gave a precision score of 79% and with hyperparamter tuning the base model did the best because the logistic regression model with hyperparamters had a precision of 78% which is stiil good but one lower than the base model. The base model, like the other models, does not predict the best for the negative(0) and neutral class(1), but it better suited for predicting the positive class(2).

## Recommendations

1. I would recommend using the base logistic regression model because it has a 79% chance of predicting accurately on positive classes from the reviews

2. I would use the base logistic regression model to predict positive classes(4 and 5 stars), but I would not use it to accurately predict negative(1 and 2 stars) and neutral(3 stars) classes.

## Next Steps

1. I want to try using lemmatization instead of porter stemmer to see if my model has a better chance of predicting the rating or maybe try using both stemmer and lemmatization

2. I want to try using a larger dataset to predict to see if my model is accurate and I would try including other types of products to not only predict on but to look at which products get the worst and best reviews

3. I would try to imporve the precision of the negative and neutral reviews by either using other models, different hyperparamters, or different preprocessing techniques
