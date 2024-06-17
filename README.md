# Predicting Stroke Risk through Machine Learning: Analysis of Biomarkers and Model Performance
 
## Abstract
Strokes are a pervasive and oftentimes fatal condition that affects millions of people around the world. Predicting strokes based on various biomarkers and risk factors can give significant insights for prevention and early intervention. This study aims to develop machine learning models to accurately predict strokes with a dataset containing 15 features and more than 4,000 entries. We performed exploratory data analysis and implemented three machine learning algorithms: K-Nearest Neighbors, Support Vector Machine, and Random Forest Classification. These models were trained on 70% of the data and tested on the remaining 30% data, with hyperparameter tuning using GridSearchCV. The best model had an accuracy of about 0.86 on the test set. Analyzing the features revealed that age, blood pressure, glucose, BMI, and cholesterol were the most significant predictors for strokes. These findings align well with the current medical knowledge and can potentially guide healthcare professionals and institutions to identify high-risk individuals for early intervention and stroke prevention. However, the models suffered in precision and recall, indicating that they must be improved before any potential use in the industry.

## Introduction
- Problem: According to the American Stroke Association, a stroke is defined as occurring when a blood vessel that allows for blood (and thus oxygen) to get to the brain is blocked by a clot or ruptures, which prevents the brain from getting the blood and oxygen it needs, causing brain cell death [1]. One in four people around the world that are over the age of 25 will have a stroke, and over 143 million years of healthy life is lost each year from stroke-related death and disability [2].
The pervasiveness of strokes as well as their lethality make them difficult to predict, since there may be different causes for different people. We felt that building models to help predict strokes based on various measurements and biomarkers may help in not only predicting strokes based on existing data, but also aid in getting a better understanding of their complex causes.
- Objectives: There were 2 main motivating factors for us when choosing this topic. First, the rates of strokes among young people are rising, and being part of that group, it seemed important to us to raise awareness for that [3]. Second, we understand the complexity of the potential causes for strokes and want to gain for ourselves (and potentially provide for others) a better understanding of what causes them, ultimately bringing more awareness to strokes in general.
Our primary objective is to build models that can accurately predict strokes based on various measurements and risk factors while also being generalizable to new data. From there, we hope to gain deeper insights into the correlations between the various explanatory variables and stroke diagnosis and explore potential causation in that regard.

## Methodology
- Acquisition: Our objective was to find a dataset that was sufficiently large enough to build robust models that was roughly 1500 entries or greater. Our chosen dataset has (15) features and over 4000 entries, which seemed to fit the criteria described above.
- Preparation: As with any dataset, we performed exploratory data analysis to understand the data, and prepare in ways that allowed the models to be trained properly. We began by looking through a small sample of the dataset and creating definitions for each of the features, as the original dataset publisher did not provide any details. Next, we checked the types of each feature and converted them to more suitable types where necessary. Then, missing values were handled. There were several features with missing values, with the highest being “Glucose” at roughly 10% of the total entries in the dataset. Crucially, there were certain entries that were missing the target variable values, which we removed. Next, we decided to use imputation to handle the remaining missing values, with the median and mode values for individual features being used to replace the numeric and categorical features, respectively. Next, we checked for negative values, but none were present in the dataset. After this, we checked for outliers using IQR and removed any entries that had values outside of the IQR for each column. Through these checks, we ensured that the models would be trained on quality data and that they would not be affected by missing values and outliers. Next, we got the data ready to be fed into the model by performing a train-test split of 70-30, using one-hot encoding to represent all the categorical features as numerical ones and then normalizing the data. Lastly, we noticed the large imbalance between the positive and negative classes in the dataset (roughly 368 and 2258 after outlier removal, respectively). To attempt to counterbalance this, we used oversampling to generate synthetic entries for the positive class.
- Model Selection: We chose to create a K-Nearest Neighbors (KNN) model, a Support Vector Machine (SVM), and a Random Forest Classification (RFC) model. KNN is a standard pick for machine learning models and we included it because it can compete with other models in terms of accuracy and work with both linear and non-linear data. It is also easy to set up and change the value of k to evaluate how that may affect the accuracy of the model. SVM is another classic machine learning model that is used heavily in the industry and in academia. We chose it because we theorized that specific explanatory variables in the dataset may result in greater separation between those who have not had a stroke and those who have had one, which SVM might benefit from. RFC was chosen because it effectively shows relationships between variables in a way that other models might not be able to. RFC's capacity to provide estimates of feature importance is invaluable for our analysis. By understanding which features most significantly impact stroke prediction, we can gain insights into risk factors and potentially guide healthcare professionals in early intervention strategies. Its versatility and ease of use make random forest an excellent candidate for exploring predictive modeling in the context of stroke. Once these models were created and fitted to our data, we evaluated the performance of each model to determine which model yielded the most accurate predictions for stroke. The models were evaluated using accuracy, precision, recall, F1-score, and a confusion matrix. Their individual hyperparameters were then tuned using GridSearchCV, which returned the best performing models within the specified ranges. We then scored the best models on the training data to observe overfitting.

## Results and Evaluation

All three models had relatively high accuracy scores (SVM: 0.74, KNN: 0.68, RFC: 0.86) but notably displayed relatively low precision scores (SVM: 0.22, KNN: 0.21, RFC: 0.47). These models also had low recall scores (SVM: 0.33, KNN: 0.53, RFC: 0.10). This means that the model could not correctly identify majority of patients who had a stroke. Because the precision and recall scores were low, the values of F1 score were also low (SVM: 0.26, KNN: 0.30, and RFC: 0.17).

Overall, KNN had the highest recall score and RFC had the highest precision score, with SVM being in the middle for both scores. RFC performed the best in terms of accuracy. However, their scores on the training data were near perfect (all above 0.9), indicating that the models overfit and do not generalize well.

All three models were correct in their predictions roughly a decent amount of the time (especially RFC), but they were prone to false positives and false negatives. In the context of the medical industry, false positives and false negatives can be quite problematic, as the former can result in unnecessary spending and treatment, while the latter can result in not treating someone that has a condition. In order to be used in the industry, these models would need to be further refined with more/higher quality data and/or more fine-tuned models and techniques, such as RandomSearchCV.

We also analyzed the list of most important features for the Random Forest Classifier and found that those features include age, blood pressure (both systolic and diastolic), glucose, BMI, and cholesterol. This aligns with the current medical understanding of strokes and what conditions may cause them as well as what measurements may indicate them.

## Visualizations
- The positive correlation suggests that, in general, as individuals age, their total cholesterol levels tend to increase. However, the correlation coefficient of 0.27 indicates that age explains only a sm all porti on of the vari ation in total cholesterol levels. Other factors beyond age likely play a more substantial role in determining total cholesterol levels. Since the correlation is weak, it implies that age alone is not a strong predictor of total cholesterol levels. Other factors such as diet, genetics, and lifestyle choices may have more significant influences on total cholesterol levels.

Image 1
Image 2

- The bar charts illustrate the difference between the observed and expected frequencies of heart strokes across genders, indicating a potential association between gender and heart stroke incidence. The Chi-square statistic of approximately 36.01 and the extremely small P-v alue (about 1.96e-09) suggest that the observed disparity is statistically significant and unlikely to be due to chance. This statistical analysis implies that gender could be an influencing factor in the occurrence of strokes.

 

## Conclusion
Overall, our goals of creating models that would operate well on new data to accurately predict stroke as well as gaining a better understanding of the cause of strokes through analyzing the most important features were somewhat realized. Our models all had relatively high accuracy scores, but they seemed to overfit. We were also able to look at the most important features for the best performing model and gain a better understanding of what explanatory variables in the dataset correlate best with the target variable. However, there is significant room for improvement. As explained previously, precision and recall scores for all 3 models were quite low, likely due to the extreme imbalance between positive and negative stroke diagnosis entries in the dataset. This was also likely the reason for the models overfitting. Thus, using a more complete dataset may help to improve these models and bring them up to a standard such that they can be directly used within the medical industry.

## Impacts

As is obvious from the name, data science involves a data driven approach to solving larger problems, and we feel that this is particularly important in the case of the medical field as a whole, as it ultimately consists of real humans and real data. Analyzing data, building models, and finding correlations can help healthcare providers and the scientific community gain a better understanding of strokes, what may cause them, and how they can help professionals with identifying strokes and their risk factors, which may ultimately save more lives. Even though the models suffer from being prone to false positives, their benefits can still be felt.

Indirectly, this project may help to raise public awareness about behaviors that may increase the risk of stroke and thus promote behavior that can mitigate that risk. Eating healthy foods that are low in saturated and trans fats as well as exercising regularly correlate with less stroke risk later in life, and promoting this behavior may also have the potential to create more general health benefits outside of stroke prevention [4].


## References
[1]: “About Stroke.” www.stroke.org. Accessed April 14, 2024. https://www.stroke.org/en/about-stroke.
[2]: Feigin, Valery L, Michael Brainin, Bo Norrving, Sheila Martins, Ralph L Sacco, Werner Hacke, Marc Fisher, Jeyaraj Pandian, and Patrice Lindsay. “World Stroke Organization (WSO): Global Stroke Fact Sheet 2022.” International Journal of Stroke 17, no. 1 (January 2022): 18–29. https://doi.org/10.1177/17474930211065917.
[3]: Bukhari, Syed, Shadi Y aghi, and Zubair Bashir. “Stroke in Y oung Adults.” Journal of clinical medicine, July 29, 2023. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10420127/.
[4]: “PreventStroke:WhatYouCanDo.”CentersforDiseaseControl and Prevention, April 5, 2022. https://www.cdc.gov/stroke/prevention.htm.
[Image 1]:“‘silent’ Heart Attacks May Help Explain Strokes of Mysterious Origin | National Institute on Aging.” “Silent” heart attacks may help explain strokes of mysterious origin, July 12, 2019. https://www.nia.nih.gov/news/silent-heart-attacks-may-help-explain- strokes-mysterious-origin.
[Image 2]:John J. Pierce, D.O. “Heart Attack and Stroke Differences - PDC.” Preventative Diagnostic Center, January 22, 2023. https://www.pdcenterlv.com/blog/the-difference-between-a-heart- attack-and-a-stroke/.
