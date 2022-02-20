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
- TF-IDF: featurizing text based on word-importance, def tfidf_model(doc_id, num_results):
- IDF: based product similarity, If title is not very big, def idf_model(doc_id, num_results):
- Till now we tried three techniques :- TF-idf > idf > BOW  (in terms of better output)

- Output look like this :

![2](https://user-images.githubusercontent.com/54996809/154860790-5b1900f4-18c1-46b0-ba84-da338fd5be4b.png)

![3](https://user-images.githubusercontent.com/54996809/154860795-ba6c6379-27f3-4634-b3c8-4c7abfbff256.png)


- Word2Vec : (featurizing text based on semantic similarity) : 
- word2vec  requires very large data corpus to work well
- we take small sample :- those word which are in our titles
- def avg_w2v_model(doc_id, num_results):
- 
- Some output was not available in BOW & tf-idf because they treated 'tiger' and 'tigers' different words
- Word2wVec gives semantics similarity (many animals print type shirt), which is not given by BOW and TfIdf

![4](https://user-images.githubusercontent.com/54996809/154861060-3e166a1d-8e3a-49a2-86a6-c184a3c65352.png)

![5](https://user-images.githubusercontent.com/54996809/154861182-79887ade-1aba-4623-83ab-2ea3cf0150cb.png)

- TF-IDF weighted Word2Vec : def weighted_w2v_model(doc_id, num_results):
- for every title we build a weighted vector representation
-
- Weighted similarity using brand and color : def idf_w2v_brand(doc_id, w1, w2, num_results):

