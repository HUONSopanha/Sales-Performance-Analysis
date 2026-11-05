# Food Delivery Data Engineering Pipeline

An end-to-end data engineering and analytics project built around a food delivery dataset. The project demonstrates how to ingest raw data, store it in both relational and NoSQL databases, transform it with Apache Spark, and perform exploratory analysis on delivery performance.

## Project Overview

This pipeline uses:

- **Kaggle** to download the food delivery dataset
- **Python and Pandas** for data loading and preparation
- **MySQL** to store structured orders and driver data
- **MongoDB** to store delivery event documents
- **PySpark** to extract, clean, transform, join, and save data
- **Parquet** to store processed datasets for analytics

The source dataset contains approximately 45,593 training orders and 11,399 test orders with information about delivery time, drivers, weather, traffic, vehicles, locations, festivals, and cities.

## Pipeline Workflow

The notebooks are intended to be executed in the following order:

1. **`1_data.ipynb`**  
   Downloads the dataset from Kaggle and verifies the raw CSV files.

2. **`2_mysql.ipynb`**  
   Creates MySQL tables and loads structured order and driver data into the `logistics_db` database.

3. **`3_mongo.ipynb`**  
   Generates delivery event records from the test data and stores them in the MongoDB `delivery_events` collection.

4. **`4_pysparkETL.ipynb`**  
   Reads data from MySQL and MongoDB, applies data cleaning and transformations, joins related datasets, and writes cleaned data to Parquet.

5. **`5_EDAandAggregation.ipynb`**  
   Reads the processed Parquet datasets and performs descriptive statistics, null-value analysis, and delivery-time aggregations.

## Data Analysis

The analysis explores relationships between delivery time and factors such as:

- Weather conditions
- Road traffic density
- Delivery distance
- Driver age and rating
- Vehicle type and condition
- Multiple deliveries
- Festivals
- City type

The processed data includes cleaned order and delivery-event datasets, with derived fields such as distance, delivery speed, normalized timestamps, and delivery duration.

## Technologies

- Python
- Jupyter Notebook
- Pandas
- PyMySQL
- PyMongo
- python-dotenv
- MySQL
- MongoDB
- Apache Spark / PySpark
- Parquet
- Kaggle API

## Prerequisites

Install and configure:

- Python 3.9+
- Jupyter Notebook or JupyterLab
- Java and Apache Spark
- MySQL Server
- MongoDB Server
- A Kaggle account and API credentials

Install the Python dependencies:

```bash
pip install pandas python-dotenv kaggle pymysql pymongo pyspark
```

## Configuration

Copy the example environment file:

```bash
copy .env.example .env
```

Update `.env` with your local database credentials and Kaggle API credentials:

```env
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=your_mysql_password
MYSQL_DATABASE=logistics_db

MONGO_HOST=localhost
MONGO_PORT=27017
MONGO_DATABASE=logistics_db
MONGO_COLLECTION=delivery_events

KAGGLE_USERNAME=your_kaggle_username
KAGGLE_KEY=your_kaggle_api_key
```

Never commit `.env` or any file containing passwords, API keys, or other credentials.

## Running the Project

1. Start MySQL and MongoDB.
2. Open the notebooks in Jupyter.
3. Configure `.env`.
4. Run the notebooks in the order listed in the **Pipeline Workflow** section.
5. Review the generated Parquet files under `data/processed`.

The Spark notebooks use local execution with all available CPU cores:

```python
.master("local[*]")
```

## Output

The ETL notebook generates:

- `data/processed/orders_clean`
- `data/processed/events_clean`

These datasets are used by the final notebook for statistical summaries and aggregation queries.

## Project Structure

```text
.
├── 1_data.ipynb
├── 2_mysql.ipynb
├── 3_mongo.ipynb
├── 4_pysparkETL.ipynb
├── 5_EDAandAggregation.ipynb
├── .env.example
└── README.md
```

## Data Source

The project uses the [Food Delivery Dataset](https://www.kaggle.com/datasets/gauravmalik26/food-delivery-dataset) available on Kaggle. Please review and comply with the dataset's license and usage conditions.

## License

This project is intended for educational and portfolio purposes. The dataset remains subject to its original Kaggle license.
