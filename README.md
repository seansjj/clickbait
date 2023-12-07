# Clickbait: News Headline Classification
Stack: Pandas | Python | Random Forest  | Tableau | XGBoost

## Objective
Classifying news networks by sensational headline score using Natural Language Processing. In doing so, also determine which news networks have the most clickbait headlines and find out what criteria best determines sensationalism.

## Rationale
Everyone encounters so much information everyday, so I wanted to originally combat news misinformation. However, developing a fact checking algorithm seemed non-feasible so I tackled sensationalized news headlines, or in modern terms - 'clickbait'. Clickbait is described by dictionary.com as "a sensationalized headline...designed to entice people".

## Process
### Collecting Info
![image](https://github.com/seansjj/news_headline_classification/assets/141446128/451ecc27-f2d0-4822-9048-b557cef80fa8)

Using the News API, I gathered headlines from 4 sources to form a baseline. Reports from All Sides, a media bias company served as a guideline in labeling Associated Press (AP), Reuters as Non-Sensational class of 0 and Buzzfeed, Entertaintment Weekly (EW) a sensational class of 1. The news dataset was from Kaggle, which someone used News API to collect data. It featured over 46000 headlines from 29 unique news sources. 

### Cleaning Data
The API data was relatively clean, so not much processing was required. Only simple tasks such as dropping duplicates, simplifying column names, and using a language detection library to remove non-english headlines was required.

### Creating Features
![image](https://github.com/seansjj/news_headline_classification/assets/141446128/3b80e551-8531-4aa8-a257-2866e9e0ce07)

Headlines were pre-processed for language analysis functions by removing the case, punctuation, non-letter characters, stop words, then changing words into their base form. The 6 features then used original or processed headlines including:
- Words in Headline
- Average Word Length: Measures how many letters in each headline word
- Average Key Word Length: Measures how many letters in each processed headline word
- Buzzword Ratio: List of common buzzwords (ex.scandal/shocking) was added to a list of top 20 most common words from buzzfeed, EW
- Unique Ratio: Ratio of unique words to total words in headline
- Uppercase Ratio: Ratio of capitalized words to total words in headline
  
### Visualizing Trends
The following plots were generated to identify patterns and trends for investigation:
- Heatmap to see correlations between both features and sensational class
- Histplots to see value distributions of features
- Boxplots to make note of extreme outliers in any features
- Scatterplot to analyze the headline length, unique ratio relationship

Afterwards, log transformation was applied on skewed distributions noted during the histplots and all features had standard scaling applied.

![image](https://github.com/seansjj/news_headline_classification/assets/141446128/da8b218c-6cf0-434b-b221-c8e72b7c0b2a)

### Evaluating Models
For this classification project, both Random Forest and XGBoost was considered. The model used train/test splits of 80/20 and was evaluated using accuracy, precision, recall via a confusion matrix and a classification report.

### Improving Predictions
Both models used random search first to find the a broad range of viable hyperparameters, then narrowed down the range using grid search.
For Random Forest, the following hyperparameters were investigated:
- Max Depth
- N Estimators
- Max Features
- Min Samples Leaf
- Min Samples Split

While for XGBoost, the following hyperparameters were investigated:
- Max Depth
- Min Child Weight
- Gamma
- Subsample
- Col Sample By Tree
- Scale POS Weight

Eventually the best parameters were found and models were evaluated with each added features and hyperparameter change. Eventually Random Forest Classifier was chosen because of its superior accuracy (0.83 to 0.81).

## Results

## Future Improvements

## Credits
- Nakatani Shuyo for their language detection library, langdetect
