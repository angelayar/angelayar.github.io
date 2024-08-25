![image](https://github.com/user-attachments/assets/d251beed-53ec-4f3c-a1bb-311019878268)---
layout: post
author: Angela Yar
title: "Enhancing Product Recommendations through Sentiment Analysis in Sephora's Beauty Products Dataset"
categories: ITD214
---
## Project Background
Sephora, a leader in the global beauty retail industry, has been at the forefront of luxury and expertise since its establishment in 1969 in Paris. Known for its diverse product range—including makeup, skincare, hair care, and beauty tools—Sephora prioritizes personalized service and expert advice. In an ever-evolving market marked by intense competition and saturation, Sephora strives to differentiate itself through innovation and customer-centric approaches. Leveraging digital tools to provide tailored recommendations is a crucial strategy for maintaining its competitive edge.

## Background
#### Business Goal
This project aims to leverage sentiment analysis to gain deeper insights into customer satisfaction with Sephora’s products. By analyzing customer reviews and ratings, the project seeks to enhance Product Recommendations: Develop a recommendation system that uses sentiment insights to suggest products more effectively, fostering cross-selling opportunities and boosting overall sales and customer satisfaction.

#### Approach
The project will use the Sephora Beauty Products dataset obtained from Kaggle, focusing on analyzing reviews and ratings to extract sentiment information. Key tasks include:

- Data Preprocessing: Clean and prepare the dataset for analysis, handling missing values, text normalization, and feature extraction.
- Sentiment Analysis: Apply natural language processing (NLP) techniques to determine the sentiment behind reviews, categorizing them into High (positive), Medium (neutral), or Low (negative) sentiments.
- Product Evaluation: Analyze sentiment trends to evaluate product performance and customer preferences.
- Recommendation System Development: Implement and refine a recommendation system that utilizes sentiment data to enhance product suggestions.

#### Expected Outcome
- Enhanced Understanding of Customer Sentiments: Detailed insights into how customers perceive different products, allowing Sephora to tailor its offerings and marketing strategies.
- Improved Product Recommendations: A robust recommendation system that leverages sentiment insights to provide personalized product suggestions, increasing cross-selling opportunities and customer satisfaction.
- Data-Driven Business Strategy: Actionable recommendations based on sentiment analysis that can guide Sephora's product development and marketing efforts, reinforcing its position as a leader in the beauty industry.

## Work Accomplished
Document your work done to accomplish the outcome

### Data Preparation
Step 1: Load Data
In Jupyter Notebook, we load the Excel CSV files into pandas data frames named products and reviews. We have intentionally excluded review4 as this will be used as unseen data for evaluating the accuracy of the sentiment prediction.

![image](https://github.com/user-attachments/assets/f9c93efb-f304-4256-a299-c25a1f223847)

Step 2: In the data exploration phase, we combined all reviews into one data frame called ‘combined_reviews’. Further checks on the data types revealed that it contains string, integers, and float. 

![image](https://github.com/user-attachments/assets/276e5c99-7778-448c-9765-48382305c283)
![image](https://github.com/user-attachments/assets/ee90b411-0f82-472e-baab-99371b3e5a77)


Step 3: Exploring the dimensions of the Products and Reviews data frame shows that there are 8494 rows and 27 columns in the Product data frame, with the number of unique values in each feature. Similarly, we performed the same dimension checks on the Reviews data frame, which contains more than 975,000 rows and 19 columns. 

![image](https://github.com/user-attachments/assets/595a5ac2-0539-47fc-8daf-f81f4e87ffa0)
![image](https://github.com/user-attachments/assets/8217787d-ecf8-4876-b0d0-02ed47e23808)

Step 4: Exploring the Descriptive statistics shows that the dataset encompasses 8,494 products, showcasing a diverse range of attributes. On average, each product has about 29,179.57 loves count, suggesting a high variance in the number of loves. Ratings are scaled between 1 to 5, with a mean of 4.19, indicating that the products generally receive favourable ratings. A mean price of $51.66 and a maximum of $1,900 indicate a significant price variation and a broad spectrum of product values. 

##### Products Data Frame
![image](https://github.com/user-attachments/assets/c4982f4f-caea-4a4f-8d9b-6a082a898a81)

##### Reviews Data Frame
![image](https://github.com/user-attachments/assets/6012d0d9-ca3e-440d-839d-8532239f4348)

The review data frame features over 975,000 entries related to product feedback. The average rating is 4.29 out of 5, and approximately 83.7% of reviews are marked as recommended. Key highlights include a substantial range in feedback count, with the maximum total feedback reaching 5,464, while the average feedback count is around 4.09. Additionally, the mean price of the products is about $48.43, ranging with minimum at $3.00 and maximum $1,900, indicating a diverse pricing spectrum. 

Step 5: Analysing the correlation in Product data frame revealed strong positive (>0.95) correlation between price_usd, value_price, and sale_price, indicating that higher prices tend to align closely with higher value and sales prices. Loves_cont has a moderate positive correlation with a review (0.68), suggesting that products with more reviews generally receive more “love” or positive feedback. Additionally, child_max_price and child_min_price show a moderate correlation (0.68), reflecting that products with higher maximum child prices also tend to have higher minimum child prices. 

![image](https://github.com/user-attachments/assets/2e393928-57f3-4d38-94f9-436a1177e29e)
Products Correlation Matrix

Correlation analysis of the Reviews data frame shows ratings has a strong positive correlation (0.85) with is_recommended, indicating that higher-rated products are more likely to be recommended by users. There is a very high correlation between total_feedback_count and total_pos_feedback_count (0.98), suggesting that products with more total feedback tend to receive a proportional amount of positive feedback. The total_neg_feedback_count shows a moderate positive correlation with total_feedback_count (0.65), implying that as the overall number of feedback increases, the number of negative feedbacks also tends to rise. 

![image](https://github.com/user-attachments/assets/a9c16928-57b6-4c43-81ce-e1b78a861c98)
Reviews Correlation Matrix

Step 6: We identified several missing values across the Products and Reviews data frames. However, not all columns are required or relevant to our business objective and analysis. Therefore, we applied feature selection or dimensionality reduction before addressing the missing values through imputation. 

![image](https://github.com/user-attachments/assets/5d76c5e4-5505-4e3d-ba54-c7dd34442ef1)

With fewer features, it reduces complexity for a more efficient imputation process. It also improves imputation accuracy with more relevant features and less noise. 

Merging the columns using “product_id” as the primary key to combine the ‘review_title’ and ‘review_text’ into one column called “merged_reviews” while retaining the source columns. The combined data frame is now called “product_reviews”; it gives the shape output of 975,094 rows and 8 columns that match the number of rows from the combined_reviews data frame.

There were missing values identified in columns of “is_recommended”, “helpfulness”, and “merged_reviews”. 

![image](https://github.com/user-attachments/assets/8716e3a6-1555-4361-b602-4b77dfb7c2b5)

It is impossible to impute text reviews, so we will put a placeholder text to replace missing reviews with “No reviews provided”, as it is easier to implement and ensures that all records have some form of text. Next, we calculate the missing values in the “is_recommended” and “helpfulness” columns using the mode by ratings. 


Step 7: It is impossible to impute text reviews, so we will put a placeholder text to replace missing reviews with “No reviews provided”, as it is easier to implement and ensures that all records have some form of text. Next, we calculate the missing values in the “is_recommended” and “helpfulness” columns using the mode by ratings. 

Step 8: We will consider dropping duplicates by keeping the first occurrence.  Instead of removing 1021 rows, the total number of rows removed is 568. 

![image](https://github.com/user-attachments/assets/0c499f03-3a57-409c-a7e4-dd9d9de53ec2)

Step 9: We will emphasize on acne products using specific keyword searches.

![image](https://github.com/user-attachments/assets/9d9553dc-b887-4e11-a93c-08d3a496b9df)

Step 10: Construct a new column to contain “high”, “medium”, and “low” sentiment levels, where ratings define these sentiment levels. If the rating is between 1 – and 2, it is categorised as low sentiment; ratings of 3 will be medium sentiment, and ratings of 4 – 5 will be high sentiment level. In a given situation, if the sentiment level is high, it equally means high ratings. 

![image](https://github.com/user-attachments/assets/84e5f77b-4ada-4dfa-8da7-4edd220ae0cd)

Step 11: We saw that the class balance on ratings and sentiment level revealed that ratings 5 is the majority class. Applying hybrid class balancing using SMOTE on the minority and under-sampling the majority class to generate a more balanced dataset. We have cleaned and balanced our dataset, which is now called the “balanced_sentiment_data”. We will make use of this data frame throughout the text preprocessing. 

![image](https://github.com/user-attachments/assets/c4a72614-59c3-4df4-a624-2bcef9b6b451)

![image](https://github.com/user-attachments/assets/9a135a54-2a67-4189-a0f2-aa4dbc8cb174)

#### Data Preprocessing

![image](https://github.com/user-attachments/assets/02472682-11bb-4c44-9a6c-f09a7d0b98aa)

Step 12: Before we begin with data preprocessing, we generated a visualization in the form of a word cloud and a frequency distribution chart. This allowed us to examine the most frequently occurring words and special characters. From the snapshot, we can see common words like “I”, “It”, “the”, “this”, “and”, “for”, and so on appear the most frequently. 

![image](https://github.com/user-attachments/assets/50326da4-f472-4eff-9c33-71616d20dc2d)
![image](https://github.com/user-attachments/assets/cab88b7e-c033-4f75-8693-f150cdb8cd32)

Firstly, stopwords do not carry important meaning or semantic information. Hence, removing it helps reduce the volume of text data and ensures relevancy and accuracy in downstream tasks. Stop word removal was applied to the following. 
•	URLS
•	Mentions (@) and hashtags (#)
•	Numbers and other special characters
•	Lowercase
•	Stopwords

![image](https://github.com/user-attachments/assets/95ca4c06-00d8-48fa-accd-f4954a898537)

Secondly, we progress to perform tokenization by dividing the text into individual units or tokens, making it easier to analyse and process the text for text analysis and machine learning. Thirdly, as accuracy is the key to our use case, we apply lemmatization instead of stemming, as this ensures the words are reduced to their proper base forms while preserving meaning. Fourthly, applying feature engineering we encode the sentiment levels to convert categorical sentiment levels (such as ‘high’, ‘medium’, and ‘low’) into numerical values which is necessary for machine learning algorithms. Having numerical sentiment values simplifies data handling and model interpretation. 

![image](https://github.com/user-attachments/assets/9be490d3-961e-4b48-80b5-1e142f556c60)

Finally, we transform text data into numerical features using TF-IDF capturing the importance of words within a document relative to a corpus collection. We begin by initialising the TF-IDF Vectorizer by ignoring common English stop words and limiting the number of terms to 10,000, which helps manage the dimensionality of the data. 

![image](https://github.com/user-attachments/assets/500295a9-ca74-4514-ab84-37868b8f1b08)



### Modelling
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

### Evaluation
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## Recommendation and Analysis
Explain the analysis and recommendations

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## AI Ethics
Discuss the potential data science ethics issues (privacy, fairness, accuracy, accountability, transparency) in your project. 

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## Source Codes and Datasets
Upload your model files and dataset into a GitHub repo and add the link here. 
https://github.com/angelayar/Test
