---
title: "Graph Neural Networks with Neptune ML (in progress)"
date: 2025-08-05
weight: 6
chapter: false
pre: "<b> 6. </b>"
---

## 🎯 Objective
Guide on exporting data from SQL Server to CSV files and manually uploading them to Amazon S3 for use in Amazon Neptune.

---

## 🧱 Step 1: Install required libraries

### Install via `pip`:

```bash
pip install pandas pyodbc boto3
```

---

## 🧩 Step 2: Connect to SQL Server and export data to the `./export` folder

### 📁 Directory structure:
```
project/
│
├── export/         # Contains CSV files after export
├── data.py         # Python script for export
```

### 🔢 Code `data.py`:

```python
import os
import pandas as pd
from sqlalchemy import create_engine

# Connection string
server = '(localdb)\\MSSQLLocalDB'
database = 'boookstore'
conn_str = f'mssql+pyodbc://@{server}/{database}?driver=ODBC+Driver+17+for+SQL+Server'

# Create connection engine
engine = create_engine(conn_str)

# List of tables to export
tables = ['dbo.Categories', 'dbo.Products', 'dbo.Orders']

# Output folder for CSV files
output_folder = './export'
os.makedirs(output_folder, exist_ok=True)

# Export each table
for table in tables:
    print(f"📌 Processing table: {table}")
    df = pd.read_sql(f"SELECT * FROM {table}", engine)
    table_name = table.split('.')[-1]
    df.to_csv(f'{output_folder}/{table_name}.csv', index=False)
    print(f"✅ Saved: {table_name}.csv")
```

---

## ☁️ Step 3: Manually upload to Amazon S3

1. Go to [AWS S3 Console](https://s3.console.aws.amazon.com/s3)
2. Create a bucket (if not already created)
3. Open the bucket → click **Upload** → select the `.csv` files in the `./export` folder
4. After uploading, copy the S3 URI of each file (e.g., `s3://your-bucket-name/Categories.csv`)
![FWD](/images/6.clean/s31.png)
![FWD](/images/6.clean/s32.png)
