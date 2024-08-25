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
