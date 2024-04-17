# Key Points on Training Data - *Designing Machine Learning Systems*

## 📋Summary:
- [Key Points on Training Data - *Designing Machine Learning Systems*](#key-points-on-training-data---designing-machine-learning-systems)
  - [📋Summary:](#summary)
    - [📌 Objective](#-objective)
    - [📚 Key Points](#-key-points)
      - [📑Insights Extracted and Descriptions:](#insights-extracted-and-descriptions)
        - [Sampling Methods](#sampling-methods)
        - [Biase and Data Quality](#biase-and-data-quality)
        - [Data Distribution and ML Performance](#data-distribution-and-ml-performance)
        - [Hand Labels](#hand-labels)
        - [Natural Labeling](#natural-labeling)
        - [Handling lack of labels](#handling-lack-of-labels)
        - [Class imbalance](#class-imbalance)
        - [Choose the right evaluation metrics](#choose-the-right-evaluation-metrics)
        - [Resampling](#resampling)
        - [Data Augmentation](#data-augmentation)
  - [📚 References](#-references)
  
### 📌 Objective

Extract and summarize 10 crucial insights about Training Data from Chapter 4 of Chip Huyen's book, ["Designing Machine Learning Systems."](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/)

---

<p align="center">
  <img width="800" src="../../Imgs/Chapter4_DMLS.png">
</p>

### 📚 Key Points 

#### 📑Insights Extracted and Descriptions:


Machine learning education often emphasizes glamorous modeling techniques, neglecting the fundamental importance of training data management. Chapter 4 of "Designing Machine Learning Systems" by Chip Huyen tackles this imbalance. It highlights how high-quality training data is the backbone of successful machine learning models. As we know, data can be messy, complex, and unpredictable. To navigate this challenge, we need techniques to acquire or create high-quality training data. Here I outline 10 crucial insights learned brought by the chapter, providing a brief yet insightful explanations to underscore its significance
	
Imagine we're building a machine learning model for forecasting. However, we're faced with a massive but messy dataset. The question arises: Where do we even begin? Sampling the data might seem like the natural first step:

##### Sampling Methods 

>Sampling, a crucial step in the machine learning workflow, enables the creation of representative training datasets, especially when dealing with limited real-world data or computationally expensive processing of the entire dataset. Non-probability sampling methods, like convenience or snowball sampling, offer a convenient approach for initial data collection, but require careful consideration of potential biases. In contrast, random sampling ensures equitable representation through methods like simple random sampling (e.g., selecting survey participants from a phonebook), stratified sampling (e.g., ensuring a proportional split of age groups in a customer survey), weighted sampling (e.g., assigning higher weights to underrepresented data points), reservoir sampling (e.g., selecting a fixed-size sample from a streaming data source), and importance sampling (e.g., prioritizing informative examples for faster model training). Overall, sampling methods play a critical role in optimizing ML processes by mitigating biases and enhancing the efficiency and representativeness of training data.

While sampling it’d be interesting to handle potential biases and the quality of the dataset:

##### Biase and Data Quality
>Biases and data quality are fundamental factors influencing the effectiveness and reliability of machine learning models. Biases within the training data can permeate the model, leading to skewed predictions and discriminatory outcomes. These biases can stem from various sources, such as data collection methods that reflect societal norms or human biases in labeling decisions.  Data quality issues further compound these biases, as inaccuracies, inconsistencies, and incompleteness can hinder model performance.  To mitigate biases and ensure data quality, comprehensive strategies are necessary. This includes rigorous data preprocessing to identify and address biases, along with thorough validation and verification processes to enhance data accuracy and reliability.  Promoting diversity and inclusivity in data collection efforts, along with adopting transparent and ethical data practices, are essential for mitigating biases and fostering high-quality data. By prioritizing bias detection and data quality assurance, machine learning practitioners can build more equitable, robust, and trustworthy models that uphold fairness and integrity in decision-making.

What about our data distribution?

##### Data Distribution and ML Performance
>Data distribution plays a critical role in machine learning (ML) model performance, impacting their ability to generalize to new data. Class imbalance, where one class significantly outnumbers others, can lead to biased models that favor the majority class and struggle with minority classes. Resampling techniques, like oversampling or undersampling, help address this by ensuring fair representation of all classes in the training data.
>
>The quality of labeled data, whether hand-labeled or obtained through natural labels, also significantly influences performance.  Hand-labeling can be expensive, time-consuming, and raise privacy concerns, while natural labels offer efficiency gains. However,  ensuring the accuracy and consistency of natural labels is crucial, as data from diverse sources can introduce biases. Additionally, the distribution of data across features can affect performance. Data augmentation techniques and algorithm-level methods can enhance model robustness to varying data distributions.
>
>Therefore, understanding and managing data distribution is fundamental for optimal ML models. This necessitates careful consideration of data preprocessing, labeling, and augmentation strategies to ensure accurate and fair representation of all classes and features in the training data.

What to do if some or all our data is not labeled?


##### Hand Labels
>Hand-labeling, a cornerstone of supervised machine learning, comes with significant costs and time investments, especially when domain expertise is needed. Privacy concerns arise  as data requires manual inspection, potentially limiting its use in scenarios with strict privacy regulations. Furthermore, hand-labeling is slow, hindering model development speed and adaptability to changing environments. Additionally, annotator variability (expertise levels) and data source diversity can lead to label inconsistencies and ambiguities. To address these issues, clear problem definitions and task rules are essential to ensure consistent and accurate labeling across annotators.  While crucial for data annotation, hand-labeling necessitates careful consideration of its challenges for optimal model development and performance.

##### Natural Labeling
>Natural labeling, harnessing inherent ground truth labels within data, offers a valuable resource for training supervised machine learning models. It expedites training and streamlines development. Tasks like recommender systems benefit greatly, as automatic or system-evaluated feedback creates shorter feedback loops and faster model adaptation. However, finding the right loop length requires balancing speed with accuracy, highlighting the complexity of optimizing labeling processes. While efficient, ensuring the quality of natural labels is crucial. Data from diverse sources can introduce inconsistencies that impact model performance. Techniques like data lineage help identify these issues by tracing data and label origins. Overall, natural labeling offers efficiency gains, but maintaining data quality and mitigating  biases remain paramount for robust and effective models.

##### Handling lack of labels
>The absence of labeled data presents hurdles in machine learning model training. Fortunately, innovative approaches address this challenge. Weak supervision utilizes labeling functions (LFs) to generate noisy labels, requiring denoising and reweighting for accuracy. Semi-supervised learning leverages existing labeled data and structural assumptions to create new labels, using methods like self-training or perturbation. Transfer learning repurposes pre-trained models for new tasks, often requiring fine-tuning. This is particularly useful for tasks with limited labeled data. Finally, active learning prioritizes labeling efficiency by letting models choose informative data points to learn from. These techniques collectively offer a toolbox to overcome limited labeled data, enabling effective machine learning model training in diverse scenarios.


Alright, so far, we've discussed how to sample our data and label it. However, we may encounter a common issue at this stage: class imbalance.

##### Class imbalance
>Class imbalance, a major hurdle in machine learning, occurs when there's a huge difference in the number of samples between classes in classification tasks. It can even impact regression tasks where specific value ranges deserve more attention. This imbalance weakens a model's ability to learn from minority classes, potentially overlooking crucial patterns.  Worse, class imbalance often carries unequal error costs. Mistakes involving rare classes can have significant consequences. Sampling biases and labeling errors can worsen the problem.
>
>To tackle this, we need specific strategies. The approach depends on the severity of imbalance and the task's sensitivity. Simpler problems might not be affected, but complex tasks require specialized techniques to ensure all classes perform well.

Regardless of whether there's a class imbalance or not, it's crucial to evaluate the model using appropriate tools to ensure a comprehensive understanding of its performance and how this is relatable to our task.

##### Choose the right evaluation metrics
>Selecting the right evaluation metrics is critical for machine learning models, regardless of class imbalance. While familiar metrics like accuracy and error rate are common, they can be misleading in imbalanced scenarios.  For example, a high accuracy might hide the model's weakness in detecting rare classes.  Therefore, metrics like F1 score, precision, and recall become crucial. These focus on the performance of the minority class, considering true positives. Additionally, plotting the ROC curve offers valuable insights. It shows the trade-off between correctly identifying positive cases and mistakenly classifying negative ones at different thresholds. By choosing appropriate metrics, practitioners gain a more comprehensive understanding of model effectiveness, enabling informed decisions for development and deployment.

##### Resampling
>Resampling techniques are a handy tool for tackling class imbalance in machine learning models. They adjust the training data distribution to help models learn better. Data-level methods like oversampling and undersampling change the class balance. Oversampling replicates minority class examples, while undersampling removes some majority class examples. Simple approaches randomly copy minority examples or remove majority ones until a desired balance is reached.
> 
>However, evaluating a model on resampled data can be misleading. Undersampling might discard valuable information, and oversampling risks memorizing the training data (overfitting).
>   
> Alternatively, algorithm-level methods keep the original data but modify the learning algorithm. Cost-sensitive learning assigns different penalties for misclassifying different classes (based on their importance).  While effective, defining these penalties can be tricky.
> 
> Resampling offers a practical approach to class imbalance, but careful consideration of its trade-offs is crucial for robust and generalizable models.

What to do if we don’t have enough data?

##### Data Augmentation
> Data augmentation is a game-changer in machine learning, especially when data is scarce. It's become a go-to technique in many fields, particularly computer vision, and is increasingly used for natural language processing (NLP) tasks as well.
> 
> Simple transformations like cropping, flipping, rotating images, or replacing words in NLP can significantly expand the training data. This makes models more robust and helps them perform better.  Data augmentation can also involve adding noise or making slight modifications to challenge the model, mimicking real-world variations.  This "adversarial training" helps identify weaknesses in the model and improve its overall performance. While less common in NLP, this strategy is still valuable for building resilience
> 
> Finally, data synthesis techniques, while not yet perfect at creating entire datasets, can still be used to generate additional data and boost model performance
> 
> In essence, data augmentation is a powerful toolbox for enriching training data, allowing models to learn better and perform well on various machine learning tasks



In conclusion, the insights extracted from Chapter 4 of Chip Huyen's book, "Designing Machine Learning Systems," shed light on crucial aspects of training data that significantly influence the effectiveness and reliability of machine-learning models. These insights, encompassing sampling methods, bias mitigation, data quality, labeling techniques, and strategies for imbalanced data and limited labels, reveal the complexities involved in crafting high-quality training datasets. Furthermore, insights into evaluation metrics, resampling, and data augmentation solidify the iterative nature of refining training data to enhance model performance and generalization. By reflecting on these insights, we recognize the pivotal role of meticulous data curation and augmentation in empowering ML algorithms to learn meaningful patterns from diverse and representative datasets, ultimately bolstering the overall effectiveness and reliability of machine-learning models in real-world applications.

## 📚 References

- [Designing Machine Learning Systems by Chip Huyen](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/)
- [Ivanovitch's repository](https://github.com/ivanovitchm/PPGEEC2318)