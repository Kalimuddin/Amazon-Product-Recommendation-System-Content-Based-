# Amazon-fashion-discovery-engine-Content-Based-recommendation :

## Problem Definition and Data Requirements :
- Main Objective is to recommend similar products in e-commerce using product content (ASIN, title, brand, color, images, type of the product, price, etc).
- Brought down number of data points from 183k to 16k by Data Cleaning.
- For text based content we used NLP techniques and for images we used Deep Learning techniques and for measuring goodness of our solution A/B testing will be a good option. 
- Required Data available at : https://drive.google.com/drive/folders/1_6GitNs8uT4G4OKkNo6Hu9-wsHcLR9a3?usp=sharing

- we have give a json file which consists of all information about the products :
- Number of data points :  183138 Number of features/variables: 19

![1](https://user-images.githubusercontent.com/54996809/154859991-638b0fc3-8053-4fd2-ba69-6a15f611ff95.png)

## Data Cleaning :
- 64956 of 183138 products have brand information. That's approx 35.4%.
- Only 28,395 (15.5% of whole data) products with price information
- Number of data points After eliminating price=NULL : 28395
- Number of data points After eliminating color=NULL : 28385
- We brought down the number of data points from 183K to 28K.
- For those of who have powerful computers and some time to spare, you are recommended to use all of the 183K images.
- Some examples of dupliacte titles that differ only in the last few words
- we have 2325 products which have same title but different color, user doesn't want to be recommended of same product of different sizes or different colors.
- Number of data points after dedupe:  16042

## Data Preprocessing :
- nltk is used alot for text pre-processing
- stopwrds removal is not good for all types of algorithm.
- we use the list of stop words that are downloaded from nltk lib.
- we take each title and we text-preprocess it.
- Stemming : Convert each of the word in root form, We tried using stemming on our titles and it didnot work very well.

## Modelling :
- Bag of Words :- bag_of_words_model(doc_id, num_results), call the bag-of-words model for a product to get similar products.
    - text based product similarity : Converting text to an n-D vector: (bag of words)
    - Bag of Words (BoW) on product titles
    - title_features.get_shape() = #data_points * #words_in_corpus, (16042, 12609)
    - Here, for each title there are 12609 columns, but in actual each titles have very less number of words, most of the column value are zero
    - we are doing BOW and euiclidean distance :-
    - if the words are more similar in titles, then euiclidean distance will be low :-
    - This BOW is not the best solution, but it is one of them solution
- 
- TF-IDF: featurizing text based on word-importance, def tfidf_model(doc_id, num_results):
-
- IDF: based product similarity, If title is not very big, def idf_model(doc_id, num_results):
-
- Till now we tried three techniques :- TF-idf > idf > BOW  (in terms of better output)

- Output look like this :

![2](https://user-images.githubusercontent.com/54996809/154860790-5b1900f4-18c1-46b0-ba84-da338fd5be4b.png)

![3](https://user-images.githubusercontent.com/54996809/154860795-ba6c6379-27f3-4634-b3c8-4c7abfbff256.png)



