# Python for AI/ML/GenAI

## Libraries

# 📘 NumPy – Arrays & Matrix Operations  

## 🔹 Introduction  

**NumPy (Numerical Python)** is a Python library for **numerical & scientific computing**.  

It provides:  
- **ndarray** → n-dimensional array object  
- **Fast mathematical operations**  
- **Tools for linear algebra, Fourier transform, random numbers**  

# 1️⃣ NumPy Arrays  

**ndarray** → Main object (similar to list but faster, supports vectorized operations).  

---

## ➤ Creating Arrays  

```python
import numpy as np  

# From list
arr = np.array([1, 2, 3])  

# Multi-dimensional
mat = np.array([[1, 2], [3, 4]])  

# Zeros, Ones, Empty
zeros = np.zeros((2, 3))   # 2x3 matrix of 0
ones = np.ones((3, 3))     # 3x3 matrix of 1
empty = np.empty((2, 2))   # random uninitialized values

# Range & linspace
r = np.arange(0, 10, 2)    # [0, 2, 4, 6, 8]
lin = np.linspace(0, 1, 5) # [0. , 0.25, 0.5 , 0.75, 1. ]
```

# 2️⃣ Array Properties  

```python
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])

arr.shape   # dimensions (rows, cols) → (2, 3)  
arr.ndim    # number of dimensions → 2  
arr.size    # total elements → 6  
arr.dtype   # data type (int, float, etc.) → int64 (depends on system)  
```


# 3️⃣ Array Operations  

## ➤ Element-wise Operations  

```python
import numpy as np  

a = np.array([1, 2, 3])  
b = np.array([4, 5, 6])  

a + b   # [5  7  9]  
a - b   # [-3 -3 -3]  
a * b   # [ 4 10 18]  
a / b   # [0.25 0.4 0.5]  
```

## ➤ Universal Functions (ufuncs)  

```python
import numpy as np  

a = np.array([1, 2, 3])  

np.sqrt(a)     # [1.    1.414  1.732]  
np.exp(a)      # exponential → [ 2.718  7.389 20.085]  
np.log(a)      # natural log → [0.     0.693  1.099]  

np.sum(a)      # sum of elements → 6  
np.mean(a)     # average → 2.0  
np.max(a)      # max value → 3  
np.min(a)      # min value → 1  
```

# 4️⃣ Indexing & Slicing  

```python
import numpy as np  

arr = np.array([[10, 20, 30],
                [40, 50, 60],
                [70, 80, 90]])  

arr[0, 1]       # 20  
arr[:, 1]       # column → [20, 50, 80]  
arr[1, :]       # row → [40, 50, 60]  
arr[0:2, 1:3]   # sub-matrix → [[20, 30],  
                #                 [50, 60]]  
```

# 5️⃣ Matrix Operations  

## ➤ Dot Product / Matrix Multiplication  

```python
import numpy as np  

A = np.array([[1, 2], [3, 4]])  
B = np.array([[5, 6], [7, 8]])  

np.dot(A, B)  
# [[19 22]  
#  [43 50]]  

A @ B   # same as dot product  
```

## ➤ Transpose  

```python
import numpy as np  

A = np.array([[1, 2], [3, 4]])  

A.T  
# [[1 3]  
#  [2 4]]  
```

## ➤ Determinant & Inverse  

```python
import numpy as np  

A = np.array([[1, 2], [3, 4]])  

np.linalg.det(A)   # determinant → -2.0  
np.linalg.inv(A)   # inverse → [[-2.   1. ]  
                   #             [ 1.5 -0.5]]  
```

## ➤ Eigenvalues & Eigenvectors  

```python
import numpy as np  

A = np.array([[1, 2], [3, 4]])  

vals, vecs = np.linalg.eig(A)  

# Eigenvalues → [-0.372,  5.372]  
# Eigenvectors → [[-0.824  -0.416]  
#                  [ 0.566  -0.910]]  
```

# 6️⃣ Random Numbers  

```python
import numpy as np  

np.random.rand(2, 2)        # uniform random numbers (0 to 1)  

np.random.randn(3, 3)       # normal distribution (mean=0, std=1)  

np.random.randint(1, 10, size=(2, 3))  # random integers between 1 and 9  
```

# 7️⃣ Advantages of NumPy  

- 🚀 **Much faster** than Python lists (uses C under the hood).  
- ⚡ **Supports vectorization** (operations on whole arrays at once).  
- 🔢 Provides **linear algebra functions**.  
- 🤖 Widely used in **Machine Learning, AI, and Data Science**.  


# 📘 Pandas – DataFrames, CSV & JSON Handling  

## 🔹 Introduction  

**Pandas (Python Data Analysis Library)** is used for **data manipulation and analysis**.  

It provides two main data structures:  
- **Series** → 1D labeled array  
- **DataFrame** → 2D labeled data (rows & columns, like Excel table)  


# 1️⃣ DataFrames  

## ➤ Creating DataFrames  

```python
import pandas as pd  

# From dictionary
data = {"Name": ["Aman", "Riya", "Karan"],
        "Age": [21, 22, 20],
        "Marks": [85, 90, 88]}  

df = pd.DataFrame(data)  
print(df)  

# From list of lists
df2 = pd.DataFrame([[1, "A"], [2, "B"]], columns=["ID", "Letter"])  
print(df2)  
```

## Output:
```python
    Name  Age  Marks
0   Aman   21     85
1   Riya   22     90
2  Karan   20     88

   ID Letter
0   1      A
1   2      B
```

## ➤ DataFrame Properties  

```python
import pandas as pd  

data = {"Name": ["Aman", "Riya", "Karan"],
        "Age": [21, 22, 20],
        "Marks": [85, 90, 88]}  
df = pd.DataFrame(data)  

df.head()     # first 5 rows  
df.tail()     # last 5 rows  
df.shape      # (rows, cols) → (3, 3)  
df.columns    # column names → Index(['Name', 'Age', 'Marks'], dtype='object')  
df.dtypes     # data types of each column  
df.info()     # summary (non-null counts, dtypes, memory usage)  
df.describe() # statistics (mean, std, min, max, quartiles)  
```

# 2️⃣ Data Selection (Indexing & Slicing)  

```python
import pandas as pd  

data = {"Name": ["Aman", "Riya", "Karan"],
        "Age": [21, 22, 20],
        "Marks": [85, 90, 88]}  
df = pd.DataFrame(data)  

df["Name"]           # select single column  
df[["Name", "Age"]]  # select multiple columns  

df.iloc[0]           # first row (by index position)  
df.loc[1, "Marks"]   # row with index=1, column="Marks"  

df[df["Marks"] > 85] # condition filter (students with Marks > 85)  
```

# 3️⃣ DataFrame Operations  

```python
import pandas as pd  

data = {"Name": ["Aman", "Riya", "Karan"],
        "Age": [21, 22, 20],
        "Marks": [85, 90, 88]}  
df = pd.DataFrame(data)  

df["Age"].mean()            # average age → 21.0  
df["Marks"].max()           # highest marks → 90  

df.sort_values("Age")       # sort by Age  

df.drop("Marks", axis=1)    # drop column "Marks"  
df.drop(0, axis=0)          # drop row with index 0  

df["Passed"] = df["Marks"] > 50  # add new column based on condition  
print(df)  
```

# 4️⃣ CSV Handling  

## ➤ Reading CSV  

```python
import pandas as pd  

# Read CSV file
df = pd.read_csv("students.csv")  
print(df)  
```
## ➤ Writing CSV  

```python
import pandas as pd  

# Write DataFrame to CSV file
df.to_csv("output.csv", index=False)  
```

# 5️⃣ JSON Handling  

## ➤ Reading JSON  

```python
import pandas as pd  

# Read JSON file
df = pd.read_json("data.json")  
print(df)  
```

## ➤ Writing JSON  

```python
import pandas as pd  

# Write DataFrame to JSON file
df.to_json("output.json", orient="records")  
```

## ➤ Writing JSON  

```python
import pandas as pd  

# Write DataFrame to JSON file
df.to_json("output.json", orient="records")  
```

# 7️⃣ Advantages of Pandas  

- 🗃️ **Easy handling** of tabular data  
- ⚡ **Fast operations** compared to pure Python  
- ❌ **Handles missing data** efficiently  
- 💾 Supports **CSV, JSON, Excel, SQL databases**  
- 📊 Widely used in **Data Science, Machine Learning, Finance, and Statistics**  


# 📘 Matplotlib & Seaborn – Plotting & Visualization  

## 🔹 Introduction  

- **Matplotlib** → Basic Python library for plotting 2D graphs  
- **Seaborn** → Built on Matplotlib, provides **beautiful statistical plots** easily  
- Used for **data visualization, analysis, and presentation**  


# 1️⃣ Matplotlib  

## ➤ Import  

```python
import matplotlib.pyplot as plt  

```

## ➤ Basic Plot  

```python
import matplotlib.pyplot as plt  

x = [1, 2, 3, 4, 5]  
y = [10, 20, 15, 25, 30]  

plt.plot(x, y)      # line plot  
plt.show()  
```

## ➤ Plot Types  

```python
import matplotlib.pyplot as plt  

x = [1, 2, 3, 4, 5]  
y = [10, 20, 15, 25, 30]  

# Line Plot
plt.plot(x, y)  

# Scatter Plot
plt.scatter(x, y)  

# Bar Plot
plt.bar(x, y)  

# Horizontal Bar Plot
plt.barh(x, y)  

# Histogram
data = [1, 2, 2, 3, 3, 3, 4]  
plt.hist(data, bins=4)  

# Pie Chart
sizes = [10, 20, 30]  
labels = ['A', 'B', 'C']  
plt.pie(sizes, labels=labels, autopct='%1.1f%%')  

plt.show()  
```

## ➤ Customization  

```python
import matplotlib.pyplot as plt  

x = [1, 2, 3, 4, 5]  
y = [10, 20, 15, 25, 30]  

plt.plot(x, y, color='red', linestyle='--', marker='o', label='Line1')  
plt.title("Line Plot")  
plt.xlabel("X-axis")  
plt.ylabel("Y-axis")  
plt.legend()  
plt.grid(True)  
plt.show()  
```

# 2️⃣ Seaborn  

## ➤ Import  

```python
import seaborn as sns  
import matplotlib.pyplot as plt  
```

## ➤ Basic Plots  

```python
import seaborn as sns  
import matplotlib.pyplot as plt  

# Load example dataset
tips = sns.load_dataset("tips")  

# Scatter Plot
sns.scatterplot(x="total_bill", y="tip", data=tips)  

# Line Plot
sns.lineplot(x="size", y="total_bill", data=tips)  

# Bar Plot
sns.barplot(x="day", y="total_bill", data=tips)  

# Histogram / Distribution
sns.histplot(tips["total_bill"], bins=10, kde=True)  

# Boxplot
sns.boxplot(x="day", y="total_bill", data=tips)  

# Pairplot (scatter matrix)
sns.pairplot(tips)  

plt.show()  
```

## ➤ Customization  

```python
import seaborn as sns  
import matplotlib.pyplot as plt  

# Set style and palette
sns.set_style("whitegrid")       # styles: darkgrid, white, ticks
sns.set_palette("pastel")        # color palettes

# Example plot
tips = sns.load_dataset("tips")
sns.scatterplot(x="total_bill", y="tip", data=tips)

plt.title("Seaborn Plot Example")  
plt.show()  
```

# 3️⃣ Key Differences  

| Feature             | Matplotlib                 | Seaborn                        |
|--------------------|---------------------------|--------------------------------|
| Complexity          | Low-level, flexible       | High-level, easier for stats   |
| Style               | Default plain             | Attractive, built-in styles    |
| Data                | Works with lists, arrays  | Works well with DataFrames     |
| Statistical plots   | Needs extra coding        | Built-in for stats             |

---

# 4️⃣ Advantages  

- **Matplotlib** → Precise control, basic & advanced plotting  
- **Seaborn** → Beautiful visualizations, statistical insight, easy with Pandas  
- Widely used in **Data Science, Machine Learning, Reporting, and Analysis**  


# 📘 Scikit-learn – Machine Learning & Model Evaluation  

## 🔹 Introduction  

**Scikit-learn (sklearn)** → Python library for **Machine Learning**  

It provides:  
- **Supervised Learning** → Regression, Classification  
- **Unsupervised Learning** → Clustering, Dimensionality Reduction  
- **Model selection & evaluation tools**  

✅ Works well with **NumPy, Pandas, and Matplotlib/Seaborn**  

# 1️⃣ Importing  

```python
import numpy as np  
import pandas as pd  

from sklearn.model_selection import train_test_split  
from sklearn.preprocessing import StandardScaler  
from sklearn.metrics import accuracy_score, confusion_matrix  
```

# 2️⃣ Supervised Learning  

## ➤ Regression  

Predict **continuous values** (e.g., house prices, salary)  

```python
from sklearn.linear_model import LinearRegression  
from sklearn.model_selection import train_test_split  

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)  

# Model training
model = LinearRegression()  
model.fit(X_train, y_train)  

# Prediction
y_pred = model.predict(X_test)  
```

## ➤ Classification  

Predict **categories / labels** (e.g., spam vs not spam)  

```python
from sklearn.ensemble import RandomForestClassifier  

# Model training
model = RandomForestClassifier()  
model.fit(X_train, y_train)  

# Prediction
y_pred = model.predict(X_test)  
```

# 3️⃣ Unsupervised Learning  

## ➤ Clustering  

```python
from sklearn.cluster import KMeans  

# KMeans clustering
kmeans = KMeans(n_clusters=3)  
kmeans.fit(X)  

# Cluster labels
labels = kmeans.labels_  
```

## ➤ Dimensionality Reduction  

```python
from sklearn.decomposition import PCA  

# Reduce dataset to 2 components
pca = PCA(n_components=2)  
X_reduced = pca.fit_transform(X)  
```

# 4️⃣ Model Evaluation  

## ➤ Regression Metrics  

```python
from sklearn.metrics import mean_squared_error, r2_score  

# Calculate metrics
mse = mean_squared_error(y_test, y_pred)  
r2 = r2_score(y_test, y_pred)  

print("Mean Squared Error:", mse)  
print("R² Score:", r2)  
```

## ➤ Classification Metrics  

```python
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report  

# Calculate metrics
acc = accuracy_score(y_test, y_pred)  
cm = confusion_matrix(y_test, y_pred)  
report = classification_report(y_test, y_pred)  

print("Accuracy:", acc)  
print("Confusion Matrix:\n", cm)  
print("Classification Report:\n", report)  
```

## ➤ Cross-Validation  

```python
from sklearn.model_selection import cross_val_score  

# 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5)  

print("Cross-validation scores:", scores)  
print("Average score:", scores.mean())  
```
# 🔹 Preprocessing & Feature Scaling  

```python
from sklearn.preprocessing import StandardScaler, LabelEncoder  

# Standardize features
scaler = StandardScaler()  
X_scaled = scaler.fit_transform(X)  

# Encode categorical labels
le = LabelEncoder()  
y_encoded = le.fit_transform(y)  
```

# 6️⃣ Pipeline (Optional but Useful)  

```python
from sklearn.pipeline import Pipeline  
from sklearn.preprocessing import StandardScaler  
from sklearn.linear_model import LogisticRegression  

# Create a pipeline: scaling + classifier
pipe = Pipeline([
    ('scaler', StandardScaler()),  
    ('classifier', LogisticRegression())  
])  

# Train and predict
pipe.fit(X_train, y_train)  
y_pred = pipe.predict(X_test)  
```

# 7️⃣ Advantages of Scikit-learn  

- ✅ **Easy-to-use ML algorithms** for beginners and professionals  
- ⚡ Supports **preprocessing, training, evaluation, and pipelines**  
- 🔢 Works seamlessly with **NumPy, Pandas, Matplotlib**  
- 🧠 Supports **classification, regression, clustering, and dimensionality reduction**  


