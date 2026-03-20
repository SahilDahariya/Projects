iphone-sales-analytics/
│
├── data/
│   └── iphone_sales.csv
│
├── notebooks/
│   └── analysis.ipynb
│
├── src/
│   ├── data_cleaning.py
│   ├── analysis.py
│   └── visualization.py
│
├── dashboard/
│   └── dashboard.pbix  (Power BI file)
│
├── reports/
│   └── summary_report.pdf
│
├── requirements.txt
├── README.md
└── main.py


📦 1. requirements.txt
pandas
numpy
matplotlib
seaborn
plotly
scikit-learn
jupyter
📊 2. Sample Dataset (iphone_sales.csv)
Date,Model,Storage,Color,Price,Units_Sold,Region,Sales_Channel
2023-01-10,iPhone 13,128GB,Black,799,50,USA,Online
2023-01-15,iPhone 14,256GB,Blue,999,40,India,Store
2023-02-05,iPhone 12,64GB,White,599,60,UK,Online
2023-02-20,iPhone 13,128GB,Red,799,30,USA,Store
2023-03-10,iPhone 14 Pro,256GB,Gold,1099,25,Germany,Online
🧹 3. data_cleaning.py
import pandas as pd

def load_data(path):
    df = pd.read_csv(path)
    return df

def clean_data(df):
    df['Date'] = pd.to_datetime(df['Date'])
    df.dropna(inplace=True)
    return df
📈 4. analysis.py
def add_revenue(df):
    df['Revenue'] = df['Price'] * df['Units_Sold']
    return df

def sales_by_model(df):
    return df.groupby('Model')['Revenue'].sum().sort_values(ascending=False)

def sales_by_region(df):
    return df.groupby('Region')['Revenue'].sum()
📊 5. visualization.py
import matplotlib.pyplot as plt
import seaborn as sns

def plot_sales_by_model(df):
    data = df.groupby('Model')['Revenue'].sum().reset_index()
    sns.barplot(x='Model', y='Revenue', data=data)
    plt.xticks(rotation=45)
    plt.title("Revenue by iPhone Model")
    plt.show()

def monthly_trend(df):
    df['Month'] = df['Date'].dt.to_period('M')
    trend = df.groupby('Month')['Revenue'].sum()
    trend.plot(kind='line', title="Monthly Revenue Trend")
    plt.show()
▶️ 6. main.py
from src.data_cleaning import load_data, clean_data
from src.analysis import add_revenue, sales_by_model
from src.visualization import plot_sales_by_model

# Load
df = load_data("data/iphone_sales.csv")

# Clean
df = clean_data(df)

# Analyze
df = add_revenue(df)

# Print results
print(sales_by_model(df))

# Visualize
plot_sales_by_model(df)
📘 7. README.md
# iPhone Sales Data Analytics Project

## 📌 Overview
This project analyzes iPhone sales data to uncover trends, revenue insights, and customer behavior.

## 🛠 Tools Used
- Python (Pandas, NumPy)
- Matplotlib, Seaborn
- Power BI

## 📊 Features
- Sales trend analysis
- Revenue calculation
- Model performance comparison
- Regional insights

## ▶️ How to Run
1. Install requirements:
   pip install -r requirements.txt

2. Run project:
   python main.py

## 📈 Output
- Visual charts
- Insights on top-selling models
- Revenue trends
📊 8. Power BI Dashboard (Optional)

Include:

KPI Cards (Total Revenue, Units Sold)

Sales Trend Line Chart

Model Comparison Bar Chart

Region Filter

🚀 9. Extra (Optional Enhancements)

Add forecasting (Prophet)

Build ML model (sales prediction)

Deploy dashboard (Streamlit)
