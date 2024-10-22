```
# Import necessary libraries
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.neighbors import KNeighborsClassifier
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
X = normalized_data.T  # Transpose to have samples as rows and genes as columns
y = metadata['IDH']  # Target labels

# Split data into training and test sets (80% training, 20% testing)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 4. Feature Selection using Variance Threshold (simple method for fast feature reduction)
from sklearn.feature_selection import VarianceThreshold

selector = VarianceThreshold(threshold=0.01)  # Remove low-variance features
X_train_selected = selector.fit_transform(X_train)
X_test_selected = selector.transform(X_test)

# 5. Train the K-Nearest Neighbors (KNN) classifier on the selected features
knn_model = KNeighborsClassifier(n_neighbors=5)  # You can adjust n_neighbors as needed
knn_model.fit(X_train_selected, y_train)

# 6. Make predictions on the test set
y_pred = knn_model.predict(X_test_selected)

# 7. Evaluate the model performance
accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy of KNN classifier: {accuracy:.2f}")

# Print confusion matrix and classification report
print("\nConfusion Matrix:")
print(confusion_matrix(y_test, y_pred))

print("\nClassification Report:")
print(classification_report(y_test, y_pred))

# 8. Save the selected genes to a file (after feature selection)
selected_genes = pd.Series(X_train.columns[selector.get_support()])
selected_genes.to_csv('selected_genes_knn.csv', index=False)


# 9. Plot the importance of the selected features
# For KNN, there is no feature importance, but we can visualize the distribution of selected features.
plt.figure()
plt.title("Distribution of Selected Features")
plt.hist(np.sum(X_train_selected, axis=0), bins=20)
plt.xlabel('Feature Value')
plt.ylabel('Frequency')
plt.show()

# 10. Create a DataFrame with results
results_df = pd.DataFrame({
    'barcode': X_test.index,  # Barcode or sample name
    'true_sample_type': y_test,  # True sample type from metadata
    'predicted_sample_type': y_pred,  # Predicted sample type
    'model_accuracy': accuracy,  # Overall accuracy of the model
    'selected_features': "; ".join(map(str, selected_genes))  # Concatenate selected feature names into a single string
})

# Display the results DataFrame
print(results_df)
```
