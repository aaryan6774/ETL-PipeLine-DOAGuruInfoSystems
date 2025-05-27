# ETL-PipeLine-DOAGuruInfoSystems

## GOALS AND EXPECTATIONS

Ingests (loads) a raw CSV of cryptocurrency transactions.
Cleans and validates the data.
Transforms it into useful summary outputs (like average prices, volumes, etc.).
Stores this in Delta Lake in three stages:
Bronze (Raw)
Silver (Cleaned)
Gold (Aggregated/Analytics)
Entire process should be automated and trackable, ideally using Databricks and shell scripts.



# 🧭 FROM START TO END: What You Are Doing
### Step	What You’re Doing	Tool or Script
1️⃣	Get the raw data (cryptodata.csv)	CSV file (Excel/OneDrive)
2️⃣	Convert Excel to CSV if needed	excel_to_csv.py
3️⃣	Validate file info: rows, columns, nulls	Shell script + Python
4️⃣	Upload file to Databricks FileStore	Databricks UI
5️⃣	Create a Bronze node	Raw Delta Tablek
6️⃣	Create a Silver node	Clean data (remove nulls)
7️⃣	Create a Gold node	Summarized: avg price etc.
8️⃣	Query/analyze Gold table	Databricks SQL
9️⃣	Show results to team/manager	Dashboard or table output


## 🔄 Medallion Architecture Used
### Layer	Data Quality	
#### What You Store	Purpose
Bronze	🔸 Raw	CSV as Delta	Never lose original data
Silver	⚪ Cleaned	Valid rows	Prepare for business use
Gold	🟡 Final	Aggregates	Used by management, ML


## Outcome They Want:
### A working, automated pipeline
They should be able to run it step by step (nodes)
Final result should give clean insights
e.g., average price of each crypto coin
most traded coin
null/missing data counts


# What Is This Project?
## building a Data Pipeline for a Cryptocurrency Transaction Dataset using:
✅ Shell scripting for initial validation
✅ Databricks for processing and analyzing data
✅ Delta Lake for managing raw → cleaned → analyzed data
✅ Notebooks as Nodes, where each node is a stage in the pipeline


## What Your Company Wants From You
### They want you to:

# 💼 Expectation	📄 Description
1. Cleanly structured data pipeline	Split your pipeline into clear stages or "nodes" that do only one task
2. Reusable & modular scripts	Each script or notebook should be reusable and independently testable
3. Bronze-Silver-Gold Data Architecture	Save data in layers as it gets cleaned and transformed
4. Quality checks	Validate raw data (duplicates, nulls, data types) before use
5. Ready for analytics or ML	After cleaning, the final "Gold" data will be used by other teams (BI/ML)


# taking messy raw data → validating it → cleaning it → storing it in layers (Bronze → Silver → Gold) → making it ready for analytics or ML.





# FILE STRUCTURE
![image](https://github.com/user-attachments/assets/71eb0791-d2b7-48ab-9b8e-d58dce63c67a)

![image](https://github.com/user-attachments/assets/1aa10b26-ad69-45b9-85a6-e1070bb8ded6)

### Create a file named validate_csv.sh and paste the following:
#!/bin/bash

echo "================= STEP 1: Data File Validation ================="

filename="cryptodata.csv"

if [ ! -f "$filename" ]; then
  echo "❌ Error: $filename not found!"
  exit 1
fi

echo -e "\n✅ File Found: $filename"

filesize=$(du -h "$filename" | cut -f1)
rows=$(cat "$filename" | wc -l)
cols=$(head -1 "$filename" | sed 's/[^,]//g' | wc -c)

echo -e "\n📂 File Size      : $filesize"
echo "🔢 Total Rows     : $((rows - 1)) (excluding header)"
echo "🔢 Total Columns  : $((cols + 1))"

echo -e "\n🧾 Column Names and Index:"
head -1 "$filename" | tr ',' '\n' | nl

echo -e "\n================= STEP 2: Summary with Python ================="
python3 utils/data_summary.py "$filename"

echo -e "\n================= ✅ VALIDATION COMPLETE ================="

### Step 1.3: Create Python summary file data_summary.py
![image](https://github.com/user-attachments/assets/02a7037d-8aa0-4864-aa64-9cb5268be4a6)
import sys
import pandas as pd

filename = sys.argv[1]
df = pd.read_csv(filename)

print("\n📊 Data Types:")
print(df.dtypes)

print("\n🔍 Missing Values per Column:")
print(df.isnull().sum())

print("\n🔁 Duplicate Rows Count:")
print(df.duplicated().sum())

print("\n🧮 Unique Values per Column:")
for col in df.columns:
    print(f"{col}: {df[col].nunique()} unique")

print("\n📌 Top 5 Rows:")
print(df.head())

print("\n📌 Bottom 5 Rows:")
print(df.tail())

print("\n🧠 Memory Usage:")
print(df.memory_usage(deep=True))

print("\n✅ Shape of DataFrame:", df.shape)


![image](https://github.com/user-attachments/assets/304537dc-13bb-4b6b-b6d1-857d728e5f9e)
![image](https://github.com/user-attachments/assets/297808d3-39f2-4476-a030-ddb9c1c98928)

![image](https://github.com/user-attachments/assets/e60d3938-dc20-4a77-8d2d-82815a94e0e7)











