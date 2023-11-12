# IDS 706 Individual Project 3 [![CI](https://github.com/nogibjj/Jaxon-Yue-Individual-Project-3/actions/workflows/cicd.yml/badge.svg)](https://github.com/nogibjj/Jaxon-Yue-Individual-Project-3/actions/workflows/cicd.yml)
### Overview
* This repository includes the components for Individual Project 3: Databricks ETL Pipeline

Demo Video
https://www.youtube.com/watch?v=nnG6vnRNmh4

### Goals
* Create a data ETL pipeline using Databricks
* Utilize Delta Lake for data storage
* Utilize Spark SQL for data transformations
* Provide data visualizations of the transformed data and data-driven recommendation
* Include an automated trigger to initiate the pipeline

### Datasets
* [Development of Average Annual Wages_1.csv (contains wages info from 2000 to 2020)](https://raw.githubusercontent.com/nogibjj/Jaxon-Yue-Mini-Project-11/main/dataset/Development%20of%20Average%20Annual%20Wages_1.csv)
* [Development of Average Annual Wages_2.csv (contains wages info from 2022)](https://raw.githubusercontent.com/nogibjj/Jaxon-Yue-Mini-Project-11/main/dataset/Development%20of%20Average%20Annual%20Wages_2.csv)

### Key elements in the repository are:
* mylib/extract.py (extracting the CSV files)
* mylib/transform_load.py (transforming and loading the dataset)
* mylib/query_viz.py (query transformation and visualization)
* Makefile
* requirements.txt
* Dockerfile
* devcontainer
* main.py
* test_main.py
* GitHub Actions

### Key Steps
1. Initialize a Databricks workspace within Azure.
2. In the Databricks Workspace, go to user settings and link your GitHub account by navigating to 'Linked Accounts'
3. Set up a global initialization script through the 'Admin Settings'. Here, define environment variables such as `SERVER_HOSTNAME` and `ACCESS_TOKEN`
4. Proceed to create a cluster that is enabled for PySpark processing
5. Clone your repository from GitHub into the Databricks workspace
6. Configure a Databricks job to establish your data pipeline, consisting of:
   * An extraction task utilizing `extract.py` from the `mylib` directory
   * A transformation and loading task using `transform_load.py` in the `mylib` directory
   * A task for running queries and generating visualizations with `query_viz.py` from the `mylib` folder

### Databricks Pipeline
1. **Data Extraction**
   * Utilizes the `requests` library to retrive the wages data from the URLs listed above
   * Downloads and stores the data in Databricks FileStore
2. **Databricks Environment Setup**
   * Establishes a connection to Databricks using respective environment variables (`SERVER_HOSTNAME` and `ACCESS_TOKEN`)
3. **Data Transformation and Load**
   * Transform the CSVs to respective Spark dataframes, then stored in the Databricks environment as Delta Lake Tables
   * Includes respective data validation checks to ensure the quality of the data
4. **Query Transformation and Visualization**
   * Performs a complex data tranformation using a predefined Spark SQL query. The query merges the two dataframes and retrieves the top 5 countries with the highest respective region average 2022 wages. The result includes wage information from year 2000, 2010, 2020 and 2022 for all countries.
   * Creates two meaningful data visualizations as shown below
5. **File Path Checking for `make test`**
   * Implements a function to check the connection with Databricks API and if a specified file path exists in Databricks FileStore
6. **Automated trigger via Git Push**
   * If a user pushes this repo, a new pipeline run will automatically be initiated

<img width="679" alt="Screenshot 2023-11-12 at 3 08 03 PM" src="https://github.com/nogibjj/Jaxon-Yue-Mini-Project-11/assets/70416390/56bb2007-0803-4003-bcdc-b7f219b4db84">

### Data Visualizations and Recommendation
<img width="623" alt="Screenshot 2023-11-12 at 12 39 31 AM" src="https://github.com/nogibjj/Jaxon-Yue-Mini-Project-11/assets/70416390/5ac4f9d3-57d2-4e43-a2f5-8801caabe8f7">

Oceania has the highest average wages, followed by North America, Europe, Asia and South America. Management should consider this when making decisions about business expansion, resource allocation, or market entry. They could investigate the underlying reasons for these disparities, such as differences in cost of living, labor laws, and economic development, to better tailor their strategies to each region.

<img width="654" alt="Screenshot 2023-11-12 at 12 39 41 AM" src="https://github.com/nogibjj/Jaxon-Yue-Mini-Project-11/assets/70416390/5b6cbcae-e068-4470-828c-1da6d5d68a2e">

This graph shows a significant increase in wages for the US compared to a moderate rise for the UK and a relatively flat trend for Japan. An actionable recommendation would be to analyze the factors contributing to the wage growth in the US, such as economic policies, industry growth, or inflation rates. Management can explore these factors to understand how they might be replicated or adapted to other regions to foster wage growth.
