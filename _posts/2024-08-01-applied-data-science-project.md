---
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

Correlation analysis of the Reviews data frame shows ratings has a strong positive correlation (0.85) with is_recommended, indicating that higher-rated products are more likely to be recommended by users. There is a very high correlation between total_feedback_count and total_pos_feedback_count (0.98), suggesting that products with more total feedback tend to receive a proportional amount of positive feedback. The total_neg_feedback_count shows a moderate positive correlation with total_feedback_count (0.65), implying that as the overall number of feedback increases, the number of negative feedbacks also tends to rise. 

![image](https://github.com/user-attachments/assets/a9c16928-57b6-4c43-81ce-e1b78a861c98)




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
