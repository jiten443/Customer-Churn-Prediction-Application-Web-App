# Customer-Churn-Prediction-Application-Web-App

Problem Statement
Your goal is to build the complete churn prediction application. This involves two main parts:

model.py: A script that prepares the data, trains an MLPClassifier model, evaluates it, and saves the trained model and scaler.
main.py: A Flask web server that loads the saved model and scaler, provides a web interface, and serves churn predictions.
Note: To train and save the model before running the web app, execute:
python model.py
File Structure:

project/
├── model.py                 <-- YOU WILL WRITE THIS
├── main.py                  <-- YOU WILL WRITE THIS
├── Modified_Churn_Modelling.csv  <-- PROVIDED TO YOU
├── templates/
│   └── index.html           <-- PROVIDED TO YOU
├── model.pkl                <-- OUTPUT (Trained Model)
└── scaler.pkl               <-- OUTPUT (Saved Scaler)
Step 1: Project Building

Your Tasks for model.py (The Model)
Your goal is to prepare the data, train a neural network model, and save the artifacts for later use.

Split and Scale Data:
Separate features (X) and target (y, which is the Exited column).
Split into train and test sets using train_test_split.
Docs: train_test_split
Scale numerical features using StandardScaler.
Docs: StandardScaler
Build and Train the Model:
Create an MLPClassifier with:
Add two hidden layers: first with 64 neurons and second with 32 neurons
Rectified Linear Unit activation function for hidden layers.
Adam optimizer for stochastic gradient-based optimization.
Learning rate: 0.01
Early stopping enabled
Maximum of 100 iterations (epochs) for training.
validation_fraction = 0.2 (use 20% of training data for validation)
n_iter_no_change = 10 (Stops training early if validation score does not improve for 10 consecutive epochs.)
alpha=0.001 → L2 regularization term (helps prevent overfitting).
random_state=42 → Ensures reproducibility of results.
Docs: MLPClassifier
Train the model and evaluate it on the test set (print accuracy and classification report).
Docs: scikit-learn: Classification Report
Docs: scikit-learn: Accuracy Score
Save the Model and Scaler:
Save the fitted scaler as scaler.pkl using Python’s pickle.
Save the trained model as model.pkl.
Docs: pickle
Your Tasks for main.py (The Web Server)
Your goal is to load the saved model and scaler and build a Flask web app that allows real-time churn predictions.

Load Artifacts:
When the server starts, load model.pkl and scaler.pkl into memory.
Create Prediction Logic:
Accept customer inputs via a form on index.html:
Geography (France/Germany/Spain)
Gender (Male/Female)
Credit Score
Age
Tenure (years of relationship)
Balance
Number of Products
Has Credit Card? (0 or 1)
Is Active Member? (0 or 1)
Estimated Salary
Convert these inputs into a pandas DataFrame with one-hot encoding consistent with the model’s training:
Geography_Germany, Geography_Spain, Gender_Male
Geography France → both Geography_* = 0
Gender Female → Gender_Male = 0
Ensure the features are ordered as during training:
['CreditScore', 'Age', 'Tenure', 'Balance', 'NumOfProducts',
 'HasCrCard', 'IsActiveMember', 'EstimatedSalary',
 'Geography_Germany', 'Geography_Spain', 'Gender_Male']
Scale and Predict:
Use the loaded scaler to transform the prepared input data.
Pass the scaled data to the loaded model’s predict and predict_proba methods.
predict returns the churn class (0 = Not Churn or 1 = Churn), and predict_proba gives the probability of churn.
Docs: predict
Docs: predict_proba
Run the Flask App:
Configure the app to run on 0.0.0.0 at port 3000.
Docs: Flask





