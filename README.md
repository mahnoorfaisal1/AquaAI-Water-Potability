# AquaAI 🌊

AquaAI is a machine learning project I built to predict whether water is potable or not based on different water-quality measurements.

I wanted to take a dataset, actually go through the whole ML process myself, and then turn the final model into something that people can interact with instead of leaving it as just a notebook.

## About the Project

The dataset has **3,276 water samples** and 10 columns. There are 9 water-quality features and 1 target variable (`Potability`).

The features are:

* pH
* Hardness
* Solids
* Chloramines
* Sulfate
* Conductivity
* Organic Carbon
* Trihalomethanes
* Turbidity

The target is binary:

* `0` → Not potable
* `1` → Potable

I started with some EDA to understand the dataset, check for missing values, and look at the distributions of the different features.

## Models I Tried

I didn't want to just train one model and call it a day, so I tried a few different classification algorithms:

* Logistic Regression
* Random Forest
* XGBoost

I compared their performance using cross-validation and experimented with their hyperparameters.

In the end, **Random Forest performed the best**, so I chose it as the final model for AquaAI.

## Final Model

The final model is a Random Forest Classifier with:

```text id="w8f3a2"
n_estimators = 500
min_samples_split = 2
min_samples_leaf = 1
max_features = None
max_depth = None
```

On the test set, it achieved an accuracy of about **67.68%**.

The final confusion matrix was:

```text id="f5r9k1"
[[265  35]
 [124  68]]
```

One thing I noticed during the project was that the Random Forest could get extremely high training accuracy while performing much lower on validation data. This helped me understand overfitting much better instead of just seeing it as something I had read about.

## Feature Importance

I also looked at the feature importances from the final Random Forest.

The top features were:

| Feature         | Importance |
| --------------- | ---------: |
| pH              |      0.136 |
| Sulfate         |      0.127 |
| Hardness        |      0.126 |
| Chloramines     |      0.117 |
| Solids          |      0.117 |
| Conductivity    |      0.096 |
| Organic Carbon  |      0.096 |
| Turbidity       |      0.092 |
| Trihalomethanes |      0.092 |

These values show which features were more useful to the model when making its predictions. They don't mean that a feature directly causes water to be potable or not potable.

## Streamlit App

After choosing the final model, I saved it using Joblib and built a Streamlit interface around it.

The app lets you enter the different water-quality measurements using sliders and then gives a potability prediction.

The saved model is loaded with:

```python id="j1x6p4"
import joblib

model = joblib.load("aquaAI_random_forest.pkl")
```

The model isn't retrained every time the app runs. It just loads the saved Random Forest and uses it to make predictions.

## Tech Stack

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* XGBoost
* Joblib
* Streamlit

## Project Structure

```text id="h2v7n9"
AquaAI/
│
├── app.py
├── aquaAI_random_forest.pkl
├── requirements.txt
├── AquaAI.ipynb
└── README.md
```

## Running It

Clone the repository:

```bash id="q8k4m2"
git clone <YOUR_REPOSITORY_URL>
cd AquaAI
```

Install the requirements:

```bash id="r3n6w1"
pip install -r requirements.txt
```

Run the app:

```bash id="p6t9c5"
python -m streamlit run app.py
```

## What I Learned

This project taught me a lot more than I expected going into it.

I got to practice:

* EDA and understanding a dataset before modeling
* preprocessing and feature scaling
* train/validation/test splitting
* comparing different ML models
* cross-validation
* hyperparameter tuning
* identifying overfitting
* looking at confusion matrices and classification reports
* feature importance
* saving a trained model with Joblib
* deploying a model through Streamlit

The biggest thing for me was probably seeing how different training and validation performance can be. At one point my Random Forest was getting **100% training accuracy**, but its validation accuracy was only around the high 60s. That made overfitting a lot more real to me than just learning the definition.

## Future Improvements

There are definitely things I'd like to improve in AquaAI.

Some of them are:

* Try a larger and more diverse dataset
* Improve the model's performance on the potable class
* Experiment more with class imbalance
* Try more systematic hyperparameter tuning
* Explore SHAP or other interpretability methods
* Eventually deploy the app publicly

## Disclaimer

AquaAI is an educational machine learning project. The prediction should not be treated as a certified water-safety assessment or a replacement for laboratory testing.
