# Movies-ETL

The purpose of this project is to produce one cleaned movies dataset that will be used to perform an algorithm that will help to predict wich of the movies being released will become popular.

We will be using Python and Pandas to perform the data wrangling and PostgreSQL to store the finished data.  There are two data sources that can be found in the resources folder: a scraped wikipedia of movies released since 1990 and movie rating data extracted from kaggle.  

To do this, she will follow the ETL process: extract the Wikipedia and Kaggle data from their respective files, transform the datasets by cleaning them up and joining them together, and load the cleaned dataset into a SQL database.  Finally, the code used can be found in: ETL_clean_kaggle_data.ipynb, ETL_clean_wiki_movies.ipynb, ETL_create_database.ipynb, and ETL_function_test.ipynb.ipynb.
