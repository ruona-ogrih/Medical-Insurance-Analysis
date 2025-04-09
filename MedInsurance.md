# Predicting the Price of Health: A Deep Dive into Medical Insurance Costs

This project explores the factors that drive medical insurance costs using a synthetic dataset from Kaggle. By combining SQL, Python, and Tableau, I analyzed patterns in insurance charges, built a predictive model, and created a dashboard to communicate key findings.

---

## 📦 Dataset
- **Source**: [Medical Insurance Cost Prediction (Kaggle)][Medical Insurance Cost Prediction (Kaggle)](https://www.kaggle.com/datasets/teertha/ushealthinsurancedataset)
- **Size**: 1,338 records
- **Columns**: age, sex, BMI, children, smoker, region, charges
- **Note**: This dataset is synthetic but mimics real-world insurance pricing behavior.

---

## 🔧 Tools Used
- **SQL (MySQL Workbench)** – for data exploration, cleaning, and aggregations
- **Python (pandas, sklearn)** – for preprocessing and linear regression modeling
- **Tableau** – for visualizing key findings in an interactive dashboard
- **Deepnote** – for notebook-based workflow

---

## 🔍 Key Insights
- **Smoking** had the highest impact on charges: smokers paid 3–4x more than non-smokers.
- **BMI** and **age** also influenced costs, especially when combined with smoking status.
- The **Southeast** region had the highest average charges among all regions.
- A basic **Linear Regression model** could reflect general trends, but more features are needed for precision.

---

## 🧾 SQL Sample Queries

**1. Null Check:**
```sql
SELECT COUNT(*) FROM insurance WHERE age IS NULL;
```

**2. Outlier Detection in BMI:**
```sql
SELECT * FROM insurance WHERE bmi > 50 OR bmi < 10;
```

**3. Average Charges by Smoking Status and Gender:**
```sql
SELECT sex, smoker, AVG(charges) AS avg_charge
FROM insurance
GROUP BY sex, smoker;
```

**4. Average Charges by Region:**
```sql
SELECT region, AVG(charges) AS avg_charge
FROM insurance
GROUP BY region;
```

**5. Charges vs National Average by Region (CTE):**
```sql
WITH national_avg AS (
  SELECT AVG(charges) AS national
  FROM insurance
)
SELECT region, 
       AVG(charges) AS regional_avg,
       (SELECT national FROM national_avg) AS national_avg,
       AVG(charges) - (SELECT national FROM national_avg) AS difference
FROM insurance
GROUP BY region;
```

---

## 🧠 Python Model Summary
Used Linear Regression to predict insurance charges:
```python
model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

**Actual vs Predicted (Sample):**
| Actual     | Predicted  |
|------------|------------|
| 8988.15    | 10382.19   |
| 28101.33   | 36850.70   |
| 1682.60    | 5910.23    |

---

## 📈 Tableau Dashboard
🔗 **[View Dashboard on Tableau Public](https://public.tableau.com/app/profile/ruona.ogrih/vizzes)** 

Includes:
- BMI vs Charges (Smoker split with trend lines)
- Average Charges by Smoker Status
- Average Charges by Region

---

## ⚠️ Limitations
- No access to clinical data or financial background (e.g. illness history, income, or plan type)
- Tableau can't model feature interactions
- Linear Regression is limited and sensitive to outliers

---

## ✅ Final Reflection
This project demonstrates the power of combining basic tools to uncover real insights from data. From SQL-based discovery to machine learning in Python and storytelling in Tableau, the end-to-end workflow provided a deep understanding of both the data and the modeling process.

---

### 🔗 Connect
Have feedback or ideas for improvement? Feel free to [connect on LinkedIn](https://www.linkedin.com/in/ruona-ogrih-967595230/).
