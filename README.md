"# S3toRedshift" 

             ┌────────────────────┐
             │ Raw CSV in S3      │
             │ s3://bucket/raw/   │
             └────────┬───────────┘
                      │
                      ▼
              ┌────────────────┐
              │ Glue Crawler 1 │────┐
              └────────────────┘    │
                                    ▼
                         ┌────────────────────┐
                         │ Glue Catalog Table │
                         │  (raw_data_db)     │
                         └────────┬───────────┘
                                  │
                                  ▼
                     ┌────────────────────────┐
                     │ Glue Job #1            │
                     │ Convert CSV → Parquet  │
                     └────────┬───────────────┘
                              │
                              ▼
              ┌──────────────────────────────────┐
              │ Parquet files in S3              │
              │ s3://bucket/parquet/sales_data/  │
              └────────┬─────────────────────────┘
                       │
                       ▼
              ┌────────────────┐
              │ Glue Crawler 2 │────┐
              └────────────────┘    │
                                    ▼
                         ┌────────────────────┐
                         │ Glue Catalog Table │
                         │ (parquet_data_db)  │
                         └────────┬───────────┘
                                  │
                                  ▼
                     ┌────────────────────────┐
                     │ Glue Job #2            │
                     │ Load Parquet → Redshift│
                     └────────┬───────────────┘
                              │
                              ▼
                   ┌────────────────────────┐
                   │ Amazon Redshift Table  │
                   │  public.sales_data     │
                   └────────────────────────┘
