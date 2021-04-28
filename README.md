## Identifying personal attacks in Wikipedia comments
Based on a baseline strawman code, this project aims to improve the accuracy score by trying out different machine learning models.

### Preprocessing
Before any "learning", let's clean up the text data a little bit!
* Text Cleanup
  * String lowercase
  * Regular expression to remove punctuations and emoji
  * String stripping to remove leading and trailing whitespace
  * CountVectorizer stop_words to remove stop words
* Annotator Selection
  * The attribute of "attack" if equals to 1
* Features
  * Bag-of-words
  * CountVectorizer

### Scaler
* class_weight: to get more "attack" cases selected
  * "non-attack" cases -> 1
  * "attack" cases -> 2

### Models & Classification Report
* LogisticRegression
[![Capture.jpg](https://i.postimg.cc/JzvMXqTd/Capture.jpg)](https://postimg.cc/WdGBLMcM)

* MultinomialNB
[![Capture.jpg](https://i.postimg.cc/vHCNLNs9/Capture.jpg)](https://postimg.cc/hfbsKMhP)

* RandomForestClassifier
[![Capture.jpg](https://i.postimg.cc/KzsNc1cL/Capture.jpg)](https://postimg.cc/phz8qXFX)

### Hyper-parameter Tuning
* Based on the results from RandomForestClassifier, used GridSearchCV to narrow the range of values for each hyperparameter.
* Before fitting the model, transformed the string to integer by utilizing OneHotEncoder. Otherwise, will get a ValueError of "Could not convert string to float".
* From the gridsearch.best_params results, added bootstrap, max_features, min_samples_leaf, min_samples_split, and n_estimators with suggested values.
* It's possibily the size of the data that I shrinked to 1000 (since the error: "MemoryError: Unable to allocate 63.5 GiB for an array with shape (92704, 91981) and data type float64"), and by changing the size of the date to 1000, caused the accuracy went down after applying the hyper-parameters tuning and it's down by 4%.
