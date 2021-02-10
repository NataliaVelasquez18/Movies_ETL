# Data Pipeline: Extract, Transform, and Load

## Business case:

A company in the live streaming business.  Their data science team would like to develop an algorithm to predict which low budget movies being released will become popular.  In order to do that it's necessary to go through the entire Data Pipeline (ETL):

1. **Extract**: data from multiple sources and formats. In our case, we have three data sources, [one file in JSON format scraped from wikipedia]("https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/Resources/wikipedia-movies.json"), [ratings]("https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/Resources/ratings.csv"), and [movies_metadata]("https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/Resources/movies_metadata.csv") both in CSV format and taken from Kaggle.com

2. **Transform**: Transform the data in order to store it on a database.  We read the data into a Pandas dataframe, used methods to remove null values and entire columns that were unnecessary for our analysis, and obtained one merged dataset with all the information we needed.  Any type of alteration performed in the data we extracted was considered a transformation.

3. **Load**: after the data is ready we transfered it into it's final destination, a **PostgreSQL** database.  This was done with Python directly by using Pandas to_SQL method and SQLAlchemy.


