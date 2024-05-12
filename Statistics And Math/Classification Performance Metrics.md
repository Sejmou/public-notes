## Binary Classification
Building blocks:
- **True Positives (TP)**: Instances correctly predicted as positive
- **True Negatives (TN)**: Instances correctly predicted as negative
- **False Positives (FP)**: Instances incorrectly predicted as positive (actually negative)
- **False Negatives (FN)**: Instances incorrectly predicted as negative (actually positive)

## Metrics
### Accuracy
Measures the overall correctness of predictions, calculated as (TP+TN)/(TP+TN+FP+FN)(TP+TN)/(TP+TN+FP+FN).
### Precision
Measures the proportion of true positive predictions among all positive predictions, calculated as TP/(TP+FP)TP/(TP+FP). It reflects the model's ability to avoid false positive errors.
### Recall/Sensitivity/True Positive Rate
Measures the proportion of true positive predictions among all actual positive instances, calculated as TP/(TP+FN)TP/(TP+FN). It reflects the model's ability to capture all positive instances.
### F1-Score
The harmonic mean of precision and recall, calculated as 2⋅(Precision⋅Recall)/(Precision+Recall)2⋅(Precision⋅Recall)/(Precision+Recall). It provides a balanced measure of a model's performance, especially when dealing with imbalanced datasets.
### Specificity (True Negative Rate)
Measures the proportion of true negative predictions among all actual negative instances, calculated as TN/(TN+FP)TN/(TN+FP).
### ROC Curve (Receiver Operating Characteristic Curve)
A graphical representation of the trade-off between the true positive rate (recall) and the false positive rate (1-specificity) at various classification thresholds.
### AUC-ROC (Area Under the ROC Curve)
A numerical measure of a model's ability to distinguish between classes, with a higher value indicating better discrimination.