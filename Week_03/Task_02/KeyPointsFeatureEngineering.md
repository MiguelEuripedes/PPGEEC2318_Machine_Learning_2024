# Detailed Summary on Feature Engineering - *Designing Machine Learning Systems*

## 📌 **Objective**

Provide a detailed summary of the chapter five, on Feature Engineering, from the book ["Designing Machine Learning Systems."](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/).

<p align="center">
  <img width="800" src="../../Imgs/Chapter5_DMLS.png">
</p>

## 📚 **Chapter Summary**

### **Feature Engineering - Introduction**

Feature engineering, the art of crafting meaningful input variables for machine learning models, stands as a cornerstone in the realm of ML engineering. As emphasized by the paper "Practical Lessons from Predicting Clicks on Ads at Facebook," the significance of selecting pertinent features cannot be overstated. Having the right features tends to give your model the biggest performance boost compared to clever algorithmic techniques such as hyperparameter tuning. Even though machine learning (ML) systems rely heavily on well-crafted features for success, there's no one-size-fits-all approach to feature engineering, the way you approach the features in your model is so important that even state-of-the-art model architectures may perform poorly with the wrong set of features. In the Chapter 5 of "Designing Machine Learning Systems" the author Chip Huyen provides us with some key best practices to follow when dealing with our model features and here I aim to bring the key strategies and techniques highlighted.

---

#### **Learned Features Versus Engineered Features**

Here we begin with a very important concept from the chapter: *“Feature engineering is the process of choosing what information to use and how to extract this information into a format usable by your ML models.”*

While deep learning offers the promise of automatically extracting features from data, it can't replace feature engineering entirely. Not all features are easily learned by algorithms, and many real-world applications don't rely on deep learning models. Therefore, we might leverage a combination of approaches:

- **Engineered features** are hand-crafted by data scientists with domain expertise. This process involves selecting relevant information from the raw data and transforming it into a format suitable for machine learning models. An example is calculating the ratio of square footage to bedrooms for house price prediction.


- **Learned features**, on the other hand, are automatically discovered by machine learning models, particularly deep learning models. These features represent complex patterns within the data that might be difficult or impossible to identify manually. For instance, in image recognition, a deep learning model might automatically learn features that help it distinguish between different objects in an image.


In essence, engineered features rely on human knowledge and domain expertise, while learned features emerge from the training process of machine learning models. Both approaches play a crucial role in building effective machine learning systems.

---

### **Feature Engineering Operations**

This section dives into some of the most essential operations you'll encounter during feature engineering. While it's not an exhaustive list, these techniques provide a strong foundation:

#### **Handling Missing Values**

A frequent challenge in working with real-world data is missing values. Not all missing data is created equal, and understanding the reasons behind missingness is crucial. The author outlines three main types: Missing Not At Random (MNAR) occurs when the missing values are related to the data itself (e.g., missing income data for high earners). Missing At Random (MAR) means missing values are unrelated to the missing data but might correlate with other variables (e.g., missing location data but having purchase history). Ideally, missing values would be Missing Completely At Random (MCAR), occurring entirely by chance.
The author emphasizes the importance of investigating the reasons behind missing values. There are two main approaches to handling missing data: imputation, which involves filling in the missing values, and deletion, which removes rows or columns with missing data. The best approach depends on the specific type of missingness and the characteristics of your data.

- Deletion and Imputation
  - Deletion and imputation are contrasting approaches to dealing with missing data. Deletion involves removing variables or data points with missing values, which can lead to loss of crucial information and bias in model predictions. On the other hand, imputation involves filling missing values with default values or statistical measures, which can introduce bias or noise but may be necessary depending on the data and model requirements. The choice between these methods depends on factors such as data characteristics and potential impact on model performance.

#### **Scaling**

Scaling your features before inputting them into your model is crucial for optimal performance. Feature scaling adjusts variables to a similar range, preventing the model from misinterpreting differences in scale between variables. This process, known as feature scaling, is simple yet impactful. Scaling can be achieved by intuitively ranging variables from 0 to 1 or by using a specified range like [-1, 1]. Additionally, normalizing variables to have zero mean and unit variance, a process called standardization, is beneficial, especially for neural network models. Skewed distributions can be addressed through techniques like log transformation, though its effectiveness varies depending on the data. However, scaling poses risks of data leakage and requires careful consideration of global statistics, such as min, max, or mean. During inference, these statistics must be reused, and significant changes may necessitate model retraining to maintain accuracy.


#### **Discretization**

Discretization, also known as quantization or binning, involves converting continuous features into discrete ones by creating buckets or categories for the data. While it's included in some methodologies, its practical utility is often questioned by experts. Discretization can help when dealing with limited training data and can be applied to discrete variables as well. However, it introduces discontinuities at category boundaries, which can be challenging to mitigate. Strategies such as using common sense, basic quantiles, or subject matter expertise may aid in determining appropriate boundaries.

#### **Encoding Categorical Features**

When dealing with categorical features, it's common to assign each category a unique number, assuming the categories remain static. However, in production, categories can change or new ones can emerge with evolving input data. One solution to this challenge is the Hashing trick, which involves using a hash function to generate a hashed value for each category, serving as its index. This approach allows for a fixed number of encoded values for a feature without needing to know the exact number of categories in advance. While hashed functions may result in collisions (two categories assigned the same index), their impact on performance is minimal, especially with a large hash space to reduce collisions. This technique can be particularly beneficial in continual learning scenarios, where models learn from ongoing production data.

#### **Feature Crossing**

Feature crossing involves combining two or more features to create new ones, which is valuable for capturing nonlinear relationships between variables. This technique is especially crucial for models like linear regression, logistic regression, and tree-based models, which struggle with learning nonlinear relationships. While less essential for neural networks, feature crossing can still aid in learning nonlinear relationships more efficiently. However, it has downsides, including increasing the feature space significantly and potentially causing overfitting as the number of features grows, necessitating caution in its application.

---

### **Data Leakage**

Data leakage occurs when information from the label is inadvertently included in the features used for prediction, but this information is not available during inference. This issue is particularly challenging because the leakage is often subtle and not immediately apparent. It poses a significant risk as it can lead to model failure even after thorough evaluation and testing.

#### **Common Causes for Data Leakage**

##### ***Randomly splitting time-correlated data***

Randomly splitting data into training, validation, and test sets can lead to leakage, especially when the data is time-correlated. To prevent this, split the data by time to ensure that future information does not influence the training process. 

##### ***Scaling before splitting***

Scaling features is important for model performance but using global statistics (mean, variance) from the entire dataset before splitting can lead to leakage. Always split the data first, then use statistics from the training set to scale all splits.

##### ***Filling in missing data with statistics from the test split***

When handling missing values, using statistics from the entire dataset, rather than just the training set, can cause leakage. Use statistics from the training set to fill missing values in all splits.

##### ***Poor handling of data duplication before splitting***

Duplicate data points in both the training and validation/test sets can occur due to data collection, merging, or oversampling. Always check for duplicates before splitting and perform oversampling after splitting.

##### ***Leakage from data generation process***

This type of leakage is related to how the data is collected and requires a deep understanding of the data collection process. Mitigate this risk by understanding the data sources and processing methods, and normalize the data to ensure consistent means and variances across different sources.

#### **Common Causes for Data Leakage**


Detecting data leakage is crucial for ensuring the reliability of machine learning models. Here are some effective methods:

- Firstly, analyze the predictive power of features by examining their correlation with the target variable. Unusually high correlations may indicate potential leakage. Investigate how these features are generated to confirm their validity.

- Secondly, conduct ablation studies to assess the importance of each feature. If removing a feature significantly decreases model performance, it may suggest either genuine importance or the presence of leakage.

- Additionally, closely monitor the impact of adding new features to the model. A significant performance boost after adding a feature could indicate genuine predictive power or potential leakage. Investigate the source and generation process of new features to verify their reliability.

- Lastly, exercise caution when using the test split. It should only be utilized for reporting final model performance. Any other use risks introducing future information into the training process, leading to potential leakage.

By implementing these strategies and maintaining vigilance throughout the data processing and modeling stages, data scientists can effectively detect and mitigate data leakage, ensuring the integrity and accuracy of their models.


---

### **Feature Engineering**


Engineering good features is essential for building robust machine learning models, but it's important to strike a balance. While adding features can improve model performance, having too many can lead to various problems:

1. ***Data Leakage:*** More features increase the risk of unintentionally including information from the target variable in the training data, leading to overfitting.
2. ***Overfitting:*** Too many features can cause the model to memorize the training data instead of learning general patterns, resulting in poor performance on unseen data.
3. ***Increased Resource Consumption:*** A large number of features can require more memory and computational resources, leading to higher costs for model deployment and inference.
4. ***Inference Latency:*** More features can increase the time it takes for the model to make predictions, especially in online prediction scenarios where latency is critical.
5. ***Technical Debt:*** Useless features can accumulate over time, becoming burdensome to maintain and potentially hindering model performance.

To evaluate whether a feature is beneficial for the model, consider two factors:

1. **Feature Importance:** Measure how much the model's performance deteriorates when removing the feature. Techniques like SHAP can provide insights into each feature's contribution to the model's predictions, aiding in feature selection and interpretability.
2. **Feature Generalization:** Ensure that features generalize well to unseen data. Consider the coverage of a feature (percentage of samples with values) and the distribution of feature values across different datasets. Features with low coverage or mismatched distributions between training and test data may not generalize effectively.

Ultimately, engineering good features requires a combination of statistical knowledge, intuition, and subject matter expertise to select features that enhance model performance and generalize well to new data.
