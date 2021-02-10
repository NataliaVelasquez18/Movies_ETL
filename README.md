# Data Pipeline: Extract, Transform, and Load

## Business case:

A company in the live streaming business.  Their data science team would like to develop an algorithm to predict which low budget movies being released will become popular.  In order to do that it's necessary to go through the entire Data Pipeline (ETL):

1. **Extract**: data from multiple sources and formats. In our case, we have two files, one in JSON format scraped from wikipedia and the other one in a CSV format taken from Kaggle.

2. **Transform**: Transform the data in order to store it on a database.  We read the data into a Pandas dataframe, used methods to remove null values and entire columns that were unnecessary for our analysis, and obtained one merged dataset with all the information we needed.  Any type of alteration performed in the data we extracted was considered a transformation.

3. **Load**: after the data is ready we transfered it into it's final destination, a **PostgreSQL** database.  This was done with Python directly by using Pandas to_SQL method but also can be done using SQLAlchemy.


