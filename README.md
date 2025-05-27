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
### Layer	Data Quality	What You Store	Purpose
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



