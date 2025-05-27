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
