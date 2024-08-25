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

Step 13: Stopwords do not carry important meaning or semantic information. Hence, removing it helps reduce the volume of text data and ensures relevancy and accuracy in downstream tasks. Stop word removal was applied to the following. 
•	URLS
•	Mentions (@) and hashtags (#)
•	Numbers and other special characters
•	Lowercase
•	Stopwords

![image](https://github.com/user-attachments/assets/95ca4c06-00d8-48fa-accd-f4954a898537)

Step 14: We perform tokenization by dividing the text into individual units or tokens, making it easier to analyse and process the text for text analysis and machine learning. Thirdly, as accuracy is the key to our use case, we apply lemmatization instead of stemming, as this ensures the words are reduced to their proper base forms while preserving meaning. Fourthly, applying feature engineering we encode the sentiment levels to convert categorical sentiment levels (such as ‘high’, ‘medium’, and ‘low’) into numerical values which is necessary for machine learning algorithms. Having numerical sentiment values simplifies data handling and model interpretation. 

![image](https://github.com/user-attachments/assets/9be490d3-961e-4b48-80b5-1e142f556c60)

Step 15: We transform text data into numerical features using TF-IDF capturing the importance of words within a document relative to a corpus collection. We begin by initialising the TF-IDF Vectorizer by ignoring common English stop words and limiting the number of terms to 10,000, which helps manage the dimensionality of the data. 

![image](https://github.com/user-attachments/assets/500295a9-ca74-4514-ab84-37868b8f1b08)

Step 16: Fit and Transform text data by applying the TF-IDF vectorizer to the ‘lemmatized_text’ column, converting text into TF-IDF matrix (X_tfidf). Stores the sentiment labels encoded numerically as y_tfidf, which will be used as the target variable for modelling. 

![image](https://github.com/user-attachments/assets/7fa8332a-19db-46cc-8374-7448d6729321)

Step 17: Apply dimensionality reduction with truncated SVD to reduce the number of features from the original TF-IDF matrix to 100 components. 

![image](https://github.com/user-attachments/assets/e2d34917-30aa-4eac-9f6b-f914be0db1a3)

Step 18: Creates the data frame of reduced features and calculates and sorts by TF-IDF scores of terms to understand term importance. 

![image](https://github.com/user-attachments/assets/4c59365c-7176-426c-8805-f04b4e930f26)

Step 19: Removal of rare and frequent words. We set the rare words threshold as 5 and the frequent words threshold as 100. Define and remove common words using the lambda function on ‘lemmatized_tokens’ to remove tokens that are listed in the common words. 

Preview of the cleaned word cloud.
![image](https://github.com/user-attachments/assets/f5448a68-45fd-4f6a-85a7-5c807e41461f)


### Modelling
Three of the five models were chosen for sentiment level prediction and modelling. These models were accessed based on their strengths and weaknesses. Additionally, computational resources and constraints were among the factors considered.  The chosen models are Multinomial Logistic Regression (MLR), Random Forest (RF) and Naïve Bayes (NB). 

![image](https://github.com/user-attachments/assets/55fe2b44-2629-4ac7-b861-9dc13b8085e3)

Before constructing the model, we divided the dataset into three parts: 70% for training, 20% for testing, and 10% for validation. The training data is used to develop the model, the validation data is employed to fine-tune the model’s hyperparameters, and the testing data is utilized to assess the model's final performance after training and tuning. 
Hyperparameter tuning will be performed using random search, which is more efficient and cost-effective in high-dimensional spaces. It offers better coverage of the hyperparameter space, enhancing the likelihood of identifying better performing hyperparameters.
Due to limitations in computational resources and challenges faced during model tuning, the parameter adjustments were meticulously planned with three separate tuning runs. The goal was to detect even the slightest trends or changes in performance, as any small variation could indicate a significant difference.

#### Mutlinomial Logistic Regression 
The results obtained after training the model shows an overall accuracy score of 75%. Strong precision (> 0.90) in predicting the ‘low’ and ‘high’ sentiment levels. However, it struggles to predict the ‘medium’ class with a precision of just 0.59. 

![image](https://github.com/user-attachments/assets/138d7c28-a6eb-42e5-a50e-c1d3b5555b40)

We adopted random search in hyperparameter tuning. By progressively increasing the regularization level in sequences of 10, 30 and 50, respectively, the models showed improvement in model performance. This is represented by the table below.

![image](https://github.com/user-attachments/assets/3997010b-0528-490b-809e-1a1d392779ea)

If this model is run on a GPU with a regularization range set between 100 and 500, it is likely to achieve even better accuracy and precision. However, we may find that the precision scores for both the 'low' and 'high' sentiment levels stabilize between 0.97 and 0.98, even with further increases in regularization. This suggests that beyond a certain point, additional regularization may have diminishing returns and may not significantly improve the precision for these classes.

![image](https://github.com/user-attachments/assets/c32e2ae2-2fc5-4c61-b768-24927143f366)


#### Random Forest
The results from training the Random Forest model indicate an overall accuracy of 82%. The model achieves a perfect precision of 1.00 for predicting both 'low' and 'high' sentiment levels. However, it faces challenges in predicting the 'medium' class, with a precision of 0.65, the lowest among the models. 

![image](https://github.com/user-attachments/assets/61c539d3-2a2d-4cce-8c42-5d283ecedf59)

Similarly, we utilized random search for hyperparameter tuning. Notably, increasing the number of trees (n-estimators) initially improved accuracy. However, when the number of trees was varied between 1 and 100, we observed a slight decrease in overall accuracy and precision. This may suggest that adding more trees could lead to diminishing returns or potential overfitting after a certain point, where the model starts to capture noise rather than underlying patterns.

![image](https://github.com/user-attachments/assets/fb2a91e6-0d2a-449c-af51-491e3a8fa240)


#### Naïve Bayes
The results from training the Naïve Bayes model show an overall accuracy of 71%. The model attains strong precision, exceeding 0.80, for predicting both low and high sentiment levels. However, it encounters difficulties with the 'medium' class, achieving a precision of 0.56. While this precision is the lowest among the models tested, it still indicates that the model struggles to predict 'medium' sentiment accurately. It suggests that further adjustments or additional data might be needed to enhance its performance in this area. 

![image](https://github.com/user-attachments/assets/0a325b1b-657e-4957-bcb0-dff30c4c535c)

Increasing the number of iterations does not affect class precision, although accuracy slightly improves. This is evident from the stable precision values despite the increase in iterations. Since Naïve Bayes depends on probabilistic calculations based on feature frequencies and class labels, raising the number of iterations to 300 does not influence precision. The model's performance is primarily driven by the underlying probabilistic relationships and feature distributions, rather than the number of iterations

![image](https://github.com/user-attachments/assets/9af0d6f1-1fa8-4ff6-9f68-18ab06257268)

The selected random forest was used to predict the sentiment level as it gave the highest accuracy of 82% among the other models. 


### Evaluation
The result of the predicted sentiment level using the extracted unseen text review data from Review4 Excel CSV file clearly shows that the medium class struggles to give the correct prediction. 

![image](https://github.com/user-attachments/assets/d4678b5e-f693-4f66-9b7f-213c6063a5c9)

The combined ‘predicted_sentiment’ into our group by data frame ‘balanced_sentiment_data’ revealed some inaccurate sentiment prediction for the ‘medium’ level. In our business objective, the product recommendation system aims to enhance the list of recommended products to target customers based on a ‘high’ sentiment level from a similar group of customers. 
We will try selecting two customers with dissimilarity in ratings and sentiment levels. The purpose is to counter-check if any recommended products would coincide with one another regardless of the sentiments and ratings. The outcome is true and correct, and only highly rated products by similar customers are recommended to target customers. Below is a snippet of the findings. 

![image](https://github.com/user-attachments/assets/1d670c7d-cfd3-4dc0-aeeb-b3f596109fa1)

![image](https://github.com/user-attachments/assets/1f03a06a-eafb-49e3-8d06-15ee733ad0df)

![image](https://github.com/user-attachments/assets/6391afdf-0176-426a-b939-d3102875a61e)

For example, customers 22358420165 will be recommended similar products with a high sentiment level from customers 22358420165 and so on. 


## Recommendation and Analysis
Some suggested recommendations to improve the model include the following:

- Adopt class weights in the random forest as ‘balanced’ to emphasize the importance of the ‘medium’ class. This addresses class imbalance, improves model sensitivity and reduces misclassification and bias.

- Apply feature engineering to explore new features or transform existing ones to capture class differences better. 

- Review data for labelling errors or inconsistencies resulting in data quality or label noise caused by inconsistency in the ‘medium’ class instances.

- Apply ensemble methods such as stacking ensemble to combine predictions of different models. 

From the enhanced product recommendation system, the target customers were indeed recommended with a list of top acne products based on the sentiment scores of products rated highly by other customers similar to the target customer. 

Both ratings and sentiments influence customer’s purchasing decisions. However, there are several factors to note. 

##### (i)	Customer prioritising functional attributes of the products over emotional sentiment
The focus is on the tangible and practical aspects of the product that fulfil specific needs or solve problems rather than the emotional or psychological appeal. Functional attributes of skin care products focus on tangible aspects like ingredient efficacy, compatibility with skin types, texture, packaging, and safety. Prioritizing these attributes helps ensure that the product performs effectively and meets the user's specific needs, ultimately leading to better outcomes and satisfaction.

##### (ii)	Price can be a decisive factor
Price is a major factor in purchasing decisions as it affects affordability, perceived value, and overall satisfaction. Consumers balance prices against their budget, perceived quality, and the value they expect to receive. Retailers and brands must consider these factors and strategically price their products to align with consumer expectations and market conditions. Understanding how price impacts decision-making helps businesses better position their products and develop effective pricing strategies to attract and retain customers

##### (iii)	High market saturation dilutes sentiments
High market saturation can dilute emotional sentiments by increasing competition, overwhelming consumers with choices, and leading to price-focused decisions. In such an environment, brands must adopt strategies that differentiate them from the competition, focus on unique value propositions, and engage with customers deeper to maintain emotional connections and stand out in the market.

##### (iv)	Sentiments are subjective
Sentiment is inherently subjective because it reflects individual emotions, perspectives, and personal experiences. This subjectivity influences how people perceive and react to products, brands, and marketing efforts. Recognising the subjective nature of sentiment is crucial for accurately interpreting feedback, tailoring marketing strategies, and understanding diverse customer perspectives. By acknowledging and addressing this subjectivity, businesses can better engage with their audience and create more effective and personalised interactions.

##### (v)	Other external factors
External factors such as economic conditions and social trends are crucial in shaping purchasing decisions. Economic factors like income levels, inflation, and employment rates influence consumers' budgets and spending behaviours. Social trends, including cultural shifts, technological advances, and social media influence, impact consumer preferences and demand. By understanding and adapting to these external factors, businesses can better align their strategies with consumer needs and market conditions, ultimately enhancing their ability to attract and retain customers.


## AI Ethics
The project collects user preferences, sentiments, and rating data for personalised recommendations. This data facilitates the understanding of user behaviours and generates relevant suggestions. However, some potential ethnic issues require discussion, including the following concerns: 

#### Privacy
It is essential to inform users about the collected data and its intended use. Users must obtain consent and have control over their data, including the option to opt-out if they choose. Additionally, it assures users of confidentiality and the secure handling of their data. This includes providing clear information about how their reviews will be used. 
However, incomplete data implies several potential issues affecting the analysis's quality and comprehensiveness.  During the data preparation phase of our project, we spotted missing text reviews but not missing ratings. For instance, missing reviews might indicate issues with user experience, such as difficulties in submitting reviews or technical problems on the platform where reviews are posted. Or perhaps it could be due to the customer feeling uncomfortable sharing detailed feedback concerning the potential misuse of their comments or simply due to time constraints. Inevitably, it can introduce biases in the analysis if there are gaps in understanding user sentiments and feedback. 
Another area of privacy concern is anonymizing and aggregating data to protect individual privacy by ensuring that personal identifiers are not disclosed and sensitive information is not exposed. In the case of our dataset, we differentiate and analyse customers by their Customer ID (Author_ID) instead of their full name or personal ID. 
Most importantly, to ensure the confidentiality and security of data used for recommendations, implement stringent security measures, including advanced encryption protocols and strict access controls. Regularly update and audit these measures to safeguard user data from unauthorised access, breaches, and other threats. Employ comprehensive monitoring and incident response strategies to address any security vulnerabilities or breaches that may arise swiftly.

#### Fairness
If sentiment analysis or recommendation systems are trained on biased datasets that underrepresent certain ethnic groups, the resulting recommendations may be skewed or discriminatory. For instance, our data contains physical characteristics such as skin tone, eye colour, skin type and hair colour. These attributes should be used to enhance, not diminish, the relevance and personalization of recommendations. It is essential to ensure that data collection processes are inclusive and representative of all ethnic groups. 
Another concern in sentiment analysis algorithms involves misinterpreting or underrepresenting sentiments expressed by different ethnic groups if the training data does not include a diverse range of linguistic and cultural contexts. Regularly testing and validating sentiment analysis models across different demographic groups helps to ensure that they accurately and fairly represent sentiments without bias.

#### Accuracy
Accuracy intersects with fairness and ethnic issues. Inaccurate or lacking diversity data can lead to biased and inaccurate outputs. For instance, if the model is trained predominantly on data from one kind of physical characteristic say skin tone, its accuracy for other groups might be compromised. We need to ensure that the data used for training and evaluation is representative of all relevant ethnic groups. High-quality, diverse datasets can improve the model’s accuracy across different demographics.
Another issue is the modelling phase, where models might be biased if not designed to handle diverse inputs. This can result in inaccurate recommendations or sentiment analyses. For instance, the training data quality and features used to train the model can influence the accuracy. The choice of model and specific approach used to train the model can affect its performance. We should consider implementing bias mitigation techniques and fairness-aware algorithms to enhance model accuracy across different groups. This includes techniques like re-weighting, data augmentation, or using fairness constraints during training.

#### Accountability
Accountability means holding individuals or organizations responsible for the actions and impacts of algorithms and systems, especially concerning fairness, accuracy, and ethical considerations. 
Organizations must define clear roles and responsibilities for managing and addressing ethnic biases and fairness concerns in AI systems. Assign accountability to teams or individuals responsible for monitoring, evaluating, and addressing bias and fairness issues. 
Implement monitoring systems to assess the performance and fairness of AI systems regularly. Establish reporting mechanisms where users can report issues related to bias or inaccuracies. 
The importance of User Empowerment is to challenge and seek redress if they believe AI systems have unfairly treated them. Provide mechanisms for users to access their data, correct inaccuracies, and appeal decisions made by AI systems. This ensures that users have a voice and that organizations are accountable for their AI decisions.

#### Transparency
Involve providing clear and accessible information about the model’s workings, including its design, data sources, training processes, and decision-making mechanisms. Also, being open about its limitations, assumptions, and potential biases in the model. 

## Source Codes and Datasets
Upload your model files and dataset into a GitHub repo and add the link here. 
https://github.com/angelayar/Test
