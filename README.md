# 🛒 E-Commerce Product Recommendation System

A machine learning project that segments e-commerce customers using **RFM (Recency, Frequency, Monetary)** analysis and predicts high-value customers using a **CatBoost classifier** — enabling smarter, data-driven product recommendations.

---

## 📌 Repository Description

> Customer segmentation and product recommendation engine built on the UCI Online Retail dataset. Uses RFM feature engineering and CatBoost gradient boosting to classify high-value customers with **99.88% accuracy**, helping businesses target the right customers with the right products.

---

## 📁 Project Structure

```
E-Commerce_Product_Recommendation/
│
├── E-Commerce_Product_Recommendation.ipynb   # Main notebook
├── Online-Retail.xlsx                        # Dataset (UCI Online Retail)
└── README.md                                 # Project documentation
```

---

## 🎯 Objective

Identify and classify high-value customers in an e-commerce setting by:
1. Engineering **RFM features** from raw transactional data
2. Training a **CatBoost binary classifier** to predict whether a customer is high-value
3. Visualizing **feature importance** to understand what drives customer value

---

## 📊 Dataset

**Source:** [UCI Online Retail Dataset](https://archive.ics.uci.edu/ml/datasets/Online+Retail)

| Column        | Description                                      |
|---------------|--------------------------------------------------|
| `InvoiceNo`   | Unique transaction ID                            |
| `StockCode`   | Product code                                     |
| `Description` | Product name                                     |
| `Quantity`    | Units purchased per transaction                  |
| `InvoiceDate` | Date and time of transaction                     |
| `UnitPrice`   | Price per unit (GBP)                             |
| `CustomerID`  | Unique customer identifier                       |
| `Country`     | Country of customer                              |

**Dataset size after cleaning:** ~4,339 unique customers (80/20 train-test split → 3,471 train / 868 test)

---

## ⚙️ Methodology

### 1. Data Preprocessing
- Dropped rows with missing values (`dropna`)
- Parsed `InvoiceDate` to datetime
- Engineered `TotalPrice = Quantity × UnitPrice`
- Filtered out cancelled orders (negative quantities removed)

### 2. RFM Feature Engineering
Aggregated per customer:

| Feature     | Definition                                              |
|-------------|---------------------------------------------------------|
| `Recency`   | Days since the customer's last purchase                 |
| `Frequency` | Number of unique invoices (purchase occasions)          |
| `Monetary`  | Total spend across all transactions                     |

### 3. Target Variable
Binary label based on `Monetary`:
- `1` → High-value customer (spend above median)
- `0` → Low-value customer (spend below or equal to median)

### 4. Model Training
**CatBoostClassifier** with the following hyperparameters:

| Parameter       | Value  |
|-----------------|--------|
| `iterations`    | 200    |
| `learning_rate` | 0.01   |
| `depth`         | 5      |

### 5. Evaluation
| Metric     | Score     |
|------------|-----------|
| Accuracy   | **99.88%** |

### 6. Feature Importance
A bar plot of CatBoost feature importances was generated to interpret which RFM feature most influenced predictions.

---

## 🛠️ Tech Stack

| Tool / Library     | Purpose                              |
|--------------------|--------------------------------------|
| `pandas`           | Data loading and manipulation        |
| `numpy`            | Numerical operations                 |
| `matplotlib`       | Plotting                             |
| `seaborn`          | Statistical visualization            |
| `scikit-learn`     | Train-test split, evaluation metrics |
| `catboost`         | Gradient boosting classifier         |
| `ipywidgets`       | Interactive notebook widgets         |

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn catboost ipywidgets openpyxl
```

### Run the Notebook
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/ecommerce-product-recommendation.git
   cd ecommerce-product-recommendation
   ```

2. Place `Online-Retail.xlsx` in the project directory and update the file path in **Cell 2** of the notebook:
   ```python
   data = pd.read_excel("Online-Retail.xlsx")
   ```

3. Launch Jupyter and run all cells:
   ```bash
   jupyter notebook E-Commerce_Product_Recommendation.ipynb
   ```

---

## 📈 Results

- The CatBoost model classified customers as high-value or low-value with **99.88% accuracy** on the test set.
- **Monetary** value was the dominant feature in the model, followed by **Recency** and **Frequency** — confirming that total spend is the strongest signal for customer value in this dataset.

---

## 🔮 Future Improvements

- [ ] Add RFM scoring (1–5 scale per dimension) for richer segmentation
- [ ] Implement collaborative filtering for actual product-level recommendations
- [ ] Add confusion matrix and classification report for deeper evaluation
- [ ] Deploy as a simple web app using Streamlit or Flask
- [ ] Hyperparameter tuning with cross-validation

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 🙌 Acknowledgements

- Dataset: [UCI Machine Learning Repository — Online Retail](https://archive.ics.uci.edu/ml/datasets/Online+Retail)
- CatBoost by [Yandex Research](https://catboost.ai/)
