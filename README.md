# Student GPA Prediction — Group 12

This project compares four basic machine learning models for predicting student GPA:

- Linear Regression
- Decision Tree Regressor
- Random Forest Regressor
- k-Nearest Neighbors (k-NN) Regressor

The aim is to understand data preparation, model training, validation, and evaluation using a synthetic student dataset.

# Dataset

Source: [Student Performance Dataset on Kaggle](https://www.kaggle.com/datasets/miadul/student-performance-dataset)

The dataset contains 5,000 synthetic student records.

We use four input features:
- StudyTimeWeekly
- Absences
- Tutoring
- ParentalSupport

The prediction target is GPA.

StudentID is excluded because it is an identifier. GradeClass is excluded because it represents GPA categories and would cause target leakage.

The dataset is not included in this repository. Download it from the source above and place synthetic_student_performance.csv in the same folder as the notebook.

## Method

- Split the data into 80% training data and 20% test data.
- Use random_state=42 for the split.
- Use five-fold cross-validation on the training data.
- Tune Decision Tree, Random Forest, and k-NN settings using GridSearchCV.
- Apply StandardScaler inside the k-NN pipeline.
- Select the final model using validation results before evaluating on the test set.

Validation RMSE is calculated as the square root of the mean fold MSE.

## Test Results

| Model | MAE | RMSE |
|---|---:|---:|
| Linear Regression | 0.4424 | 0.5106 |
| Decision Tree | 0.4585 | 0.5293 |
| Random Forest | 0.4485 | 0.5151 |
| k-NN | 0.4480 | 0.5133 |

Both metrics are measured in GPA points. Lower values indicate better predictions.

Linear Regression achieved the lowest validation and test RMSE. The differences between models are small; we did not test their statistical significance.

## Repository Files

- student_gpa_prediction.ipynb — complete project notebook
- figures/ — model comparison and prediction plots
- results/validation_comparison.csv — validation results
- results/test_comparison.csv — final test results

## How to Run

1. Download this repository using Code → Download ZIP and extract it.
2. Download the dataset from Kaggle.
3. Place synthetic_student_performance.csv beside the notebook.
4. Install the required packages in your Python environment:

   python -m pip install jupyterlab pandas numpy matplotlib scikit-learn

5. Start JupyterLab from the project folder:

   jupyter lab

6. Open student_gpa_prediction.ipynb.
7. Restart the kernel and run all cells from top to bottom.

The notebook creates the figures and results folders and saves the output files. Results may vary slightly between library versions.

## Limitations

The dataset is synthetic, so these results do not demonstrate how the models would perform on real students. The analysis identifies predictive patterns and does not establish causal relationships.

Only four input features are used. ParentalSupport is treated as a numeric variable with equally spaced levels.
