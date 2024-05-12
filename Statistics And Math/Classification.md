Classification is a supervised method in Machine Learning and Data Analysis. Instead of predicting a continuous value for every observation (which is the task of linear regression), the goal is to predict a _discrete_ value from a _discrete set_ $\mathcal{G}$ with $K$ values. This means that there are $K$ groups observations in the training data can belong to and $K$ groups a new test set observation can be assigned to. Instead of 'groups' other terms like 'class labels', or simply 'labels', 'classes' are also commonly used.

## Difference to Clustering
Contrary to Clustering, the labels are already known (at least for the training set), which makes classification a supervised (rather than unsupervised) approach. Clustering would try to 'find $k$ 'clusters' of elements with similar features, without having labels beforehand. So, in a way, clustering tries to find labels for observations while classification tries to find features that are characteristic for pre-defined labels.
## Types of Classification
Classification can be done in several ways. The choice of classification technique depends on the nature of the problem, the type of data available, and the specific requirements of the application.

For every type of classification, there's different [performance metrics](Classification%20Performance%20Metrics.md) that should be used. They are commonly extensions/generalizations of the metrics for the most basic type of classification which is...
### Binary Classification
This is the simplest form of classification. The goal is to categorize data into one of two possible classes or categories, so $K=2$.

Examples:
- spam email detection (spam or not spam)
- disease diagnosis (disease or no disease)
- sentiment analysis (if we restrict it to positive or negative sentiment).

For binary classification, it is often sufficient to train a single classifier for the 'positive' class. If it the classifier is not _confident enough_ that a given observation belongs to this class, it is simply assigned to the 'negative' class.
### Multi-Class Classification
This involves categorizing data into more than two **mutually exclusive** classes or categories.

Examples:
- handwritten digit recognition (0-9)
- image classification into multiple object categories, and language identification (identifying the language of a given text)

### Multi-label Classification
This is an extension of multi-class classification where each data point can belong to **multiple classes simultaneously**.

Examples:
- tagging images with multiple labels (e.g., "sunset," "beach," "ocean")
- classifying articles into multiple topics

### Ordinal Classification
In ordinal classification, the classes have a natural order or hierarchy (i.e. they are ordinal variables) and the model should predict the relative order of the classes. 

Examples:
- customer satisfaction ratings (e.g., "low," "medium," "high")
- educational degree classifications (e.g., "bachelor's," "master's," "Ph.D.")
- movie ratings

### Multi-Output Classification
Multi-output classification, also known as multi-task or multi-label multi-class classification, involves predicting multiple output variables, where each output can have multiple classes.

Examples:
- object detection in images (predicting multiple object categories and their locations)
- language translation (translating one language into multiple target languages)

### Hierarchical Classification
Hierarchical classification organizes classes into a hierarchical structure, where classes are arranged in a tree-like hierarchy. It's useful when there are fine-grained and coarse-grained class distinctions.

Examples:
- product categorization in e-commerce
- species classification (e.g., Kingdom > Phylum > Class > Order > Family > Genus > Species)

### Anomaly Detection (One-Class Classification)
Anomaly detection involves identifying rare and abnormal instances that do not conform to the expected patterns in the data.

Examples:
- fraud detection
- network intrusion detection
- quality control

## Challenges

### Class Imbalance
If the distribution of classes in the dataset is skewed, with one class having significantly fewer samples than the others, we need to account for it.

Specialized techniques are used to handle imbalanced datasets to ensure that the model doesn't bias towards the majority class. This is especially true for fraud detection or detection of rare diseases, where the 'class of interest' is far less common.

### Precision-Recall Tradeoff
TODO

## Decision Boundaries
[great explanation by Andrew Ng](https://youtu.be/iBi9zEUBs8Q?si=-kYbQiFxEa9TqIQx)
decision boundaries are defined by our hypothesis and the parameters. We define the hypothesis beforehand and find the correct parameters through the training process.

## Linear vs. Non-linear
Decision boundaries can be either linear or non-linear. (Non-) linearity is defined by the relationship between the input features and the output classes or categories.

### Linear
A linear decision boundary is a straight line (in two dimensions), a hyperplane (in higher dimensions), or a linear combination of features. It separates classes by applying a linear function of the input features. Mathematically, it can be expressed as:
$$w_1x_1 + w_2x_2 + \ldots + w_nx_n + b = 0$$
where $x_1, x_2, \ldots, x_n$ are the input features, $w_1, w_2, \ldots, w_n$ are the corresponding weights, and $b$ is the bias term. This equation describes a hyperplane in an $n$-dimensional space that separates different classes.

Linear decision boundaries are simple and have a constant slope throughout the feature space. Linear classifiers like logistic regression and linear support vector machines create linear decision boundaries by optimizing linear combinations of features.
### Nonlinear
A nonlinear decision boundary is a curve, surface, or any non-straight shape that separates classes in the feature space. It arises when the relationship between the input features and the output classes is not adequately captured by a linear function. Nonlinear decision boundaries can take various forms, such as circles, ellipses, parabolas, hyperbolas, or any complex shape.

An example for a non-linear decision boundary would be for example:
$$w_1x_1^2 + w_2x_2 + w_3\sin(x_3) + \ldots + b = 0$$
This equation includes non-linear terms like $x_1^2$ and $\sin(x_3)$, which introduce curvature or other non-linear effects to the decision boundary.

Models like decision trees, random forests, k-nearest neighbors, and support vector machines with nonlinear kernels (e.g., radial basis function kernel) can create nonlinear decision boundaries. Neural networks with nonlinear activation functions can also model nonlinear decision boundaries effectively.

### Notes
What makes a decision boundary linear or nonlinear ultimately depends on the complexity of the underlying data and the modeling capabilities of the chosen classifier or algorithm. Linear decision boundaries are appropriate when the relationship between features and classes is approximately linear, while nonlinear decision boundaries are needed when the relationship is more intricate and nonlinear.

In practice, it's essential to choose the appropriate model based on the data characteristics, as overly simplistic models (e.g., linear classifiers for highly nonlinear data) may underfit, while overly complex models (e.g., deep neural networks for simple linear problems) may overfit. Model selection and validation are crucial steps in determining the best approach for a given classification task.