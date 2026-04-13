📊 YouTube Data Pipeline (AWS End-to-End)

This project builds an end-to-end data pipeline using AWS services to ingest, process, and analyze YouTube trending data across multiple regions.

🚀 Project Overview

The pipeline follows a modern data engineering architecture:

Ingestion Layer (Bronze) → Raw CSV/JSON files uploaded to S3
Processing Layer (Silver) → AWS Lambda converts CSV to Parquet
Orchestration → AWS Step Functions
Data Quality Checks → Custom validation scripts
Storage → Amazon S3 (partitioned by region)
🏗️ Architecture
Local Data → S3 (Bronze)
                ↓
          AWS Lambda
        (CSV → Parquet)
                ↓
        S3 (Silver Layer)
                ↓
        Glue / Athena (future)
📁 Project Structure
youtube-datapipeline-2026/
│
├── data/                          # Raw dataset (CSV + JSON)
├── data_quality/                  # Data validation scripts
│   └── dq_lambda.py
│
├── lambdas/
│   └── json_to_parquet/
│       └── lambda_function.py     # CSV → Parquet conversion
│
├── glue_jobs/                     # Glue scripts (future use)
│
├── scripts/
│   ├── aws_copy.sh                # S3 upload automation
│   └── information.md
│
├── step_functions/
│   └── pipeline_orchestration.json
│
└── README.md
⚙️ Technologies Used
AWS S3 → Data storage (Bronze & Silver layers)
AWS Lambda → Data transformation (CSV → Parquet)
AWS CLI → Data upload & automation
Python (Pandas, Boto3) → Data processing
AWS Step Functions → Pipeline orchestration
Git & GitHub → Version control
📥 Data Ingestion

Data is uploaded from local system to S3 using AWS CLI:

aws s3 cp . s3://yt-datapipeline-bronze-nvirginia/youtube/raw_statistics/ --recursive

Data is partitioned by region:

region=us/
region=in/
region=gb/
🔄 Data Transformation

An AWS Lambda function is triggered on file upload:

Reads CSV from S3
Converts to Parquet using Pandas
Writes output to Silver bucket

Benefits of Parquet:

Columnar format
Faster querying
Reduced storage cost
📊 Data Quality

Custom validation logic ensures:

Schema consistency
Missing value checks
Data integrity before processing
🔁 Orchestration

AWS Step Functions manages workflow:

Trigger ingestion
Run transformation
Handle failures/retries
🔐 IAM & Permissions
s3:GetObject → Read from Bronze bucket
s3:PutObject → Write to Silver bucket
Lambda execution role configured with required access
📈 Future Enhancements
AWS Glue Crawlers for schema detection
Athena for SQL-based querying
Dashboarding (QuickSight / Power BI)
CI/CD pipeline for deployment
💡 Key Learnings
Built an event-driven pipeline using AWS
Implemented data lake architecture (Bronze → Silver)
Worked with real-world data partitioning strategies
Automated ingestion using AWS CLI
📌 How to Run
Upload data to S3 (Bronze)
Trigger Lambda (automatically via S3 event)
Verify Parquet files in Silver bucket
Query using Athena (optional)
👤 Author

Biplab Kachhap
Aspiring Data Engineer | Python | AWS | ETL
