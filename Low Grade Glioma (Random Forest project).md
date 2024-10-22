```
# Import necessary libraries
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.ensemble import RandomForestClassifier
from sklearn.feature_selection import RFE
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
import matplotlib.pyplot as plt

# Load metadata and normalized data using the direct download links
normalized_data_url = 'https://drive.google.com/uc?id=1E7xFeh2C7IYG4dTW8bCwfABJphAKHq0_'
metadata_url = 'https://drive.google.com/uc?id=1VqL4hjYY4vcRcneaKRP9rKg7Zc3NCwLy'

# Load the data into pandas DataFrames
normalized_data = pd.read_csv(normalized_data_url)
metadata = pd.read_csv(metadata_url)

# 2. Prepare data for ML
# Set the Barcode as the index for metadata
metadata.set_index('Barcode', inplace=True)

# Ensure the Barcode match between normalized data and metadata
common_samples = normalized_data.columns.intersection(metadata.index)

# Subset both datasets to include only common samples
normalized_data = normalized_data[common_samples]
metadata = metadata.loc[common_samples]

# 3. Set the classification target
# Using "IDH" as the target
X = normalized_data.T # Transpose to have samples as rows and genes as columns
y = metadata['IDH'] # Target labels

# Split data into training and test sets (80% training, 20% testing)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 4. Perform Feature Selection using Recursive Feature Elimination (RFE)
# Define Random Forest as the estimator
rf = RandomForestClassifier(n_estimators=100, random_state=42)

# Train the Random Forest on the training data
rf.fit(X_train, y_train)

# Get the feature importance from the trained Random Forest model
importances = rf.feature_importances_

# Create a DataFrame to hold feature names and their importance scores
feature_importance_df = pd.DataFrame({
    'Feature': X_train.columns,
    'Importance': importances
})

# Sort the DataFrame by importance in descending order to get the top 100 features
top_100_features = feature_importance_df.sort_values(by='Importance', ascending=False).head(100)

# Display the top 100 important features
print(top_100_features)

# Filter the dataset to only include the top 100 features
selected_features = top_100_features['Feature'].tolist()
X_train_selected = X_train[selected_features]
X_test_selected = X_test[selected_features]

# 5. Train the Random Forest classifier on the selected features
rf_model = RandomForestClassifier(n_estimators=100, random_state=42)
rf_model.fit(X_train_selected, y_train)

# 6. Make predictions on the test set
y_pred = rf_model.predict(X_test_selected)

# 7. Evaluate the model performance
accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy of Random Forest classifier: {accuracy:.2f}")

# Print confusion matrix and classification report
print("\nConfusion Matrix:")
print(confusion_matrix(y_test, y_pred))

print("\nClassification Report:")
print(classification_report(y_test, y_pred))

# 8. Save the selected genes to a file
selected_genes = pd.Series(selected_features)
selected_genes.to_csv('selected_genes.csv', index=False)

# 9. Plot the importance of the selected features
importances = rf_model.feature_importances_
indices = np.argsort(importances)[::-1][:10] # Top 10 features

# Plot top 10 important features
plt.figure()
plt.title("Top 10 Feature Importances")
plt.bar(range(10), importances[indices], align="center")
plt.xticks(range(10), [selected_features[i] for i in indices], rotation=90)
plt.show()

# Create a DataFrame with results
results_df = pd.DataFrame({
    'barcode': X_test_selected.index,  # Barcode or sample name
    'true_sample_type': y_test,  # True sample type from metadata
    'predicted_sample_type': y_pred,  # Predicted sample type
    'model_accuracy': accuracy,  # Overall accuracy of the model
    'selected_features': "; ".join(map(str, selected_features))  # Concatenate selected feature names into a single string
})

# Display the results DataFrame
print(results_df)
```
