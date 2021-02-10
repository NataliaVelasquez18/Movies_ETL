# Data Pipeline: Extract, Transform, and Load

## Business case:

A company in the live streaming business.  Their data science team would like to develop an algorithm to predict which low budget movies being released will become popular.  In order to do that it's necessary to go through the entire Data Pipeline (ETL):

1. **Extract**: data from multiple sources and formats. In our case, we have three data sources [one file in JSON format scraped from wikipedia](https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/Resources/wikipedia-movies.json), the second [ratings.csv](https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/Resources/ratings.csv), and the third [movies_metadata.csv]("https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/Resources/movies_metadata.csv") both taken from Kaggle.com


2. **Transform**: Transform the data in order to store it on a database.  We read the data into a Pandas dataframe, used methods to remove null values and entire columns that were unnecessary for our analysis, and obtained one merged dataset with all the information we needed. 


The following is the code used


* [Cleaning kaggle data](https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/ETL_clean_kaggle_data.ipynb)
* [Cleaning wikepedia dataset](https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/ETL_clean_wiki_movies.ipynb)
* [Read and visualize cleaned datasets](https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/ETL_function_test.ipynb.ipynb)
* [Merge datasets and create database](https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/ETL_create_database.ipynb)



Final merge


```
    # Merge the ratings DataFrame into clean Movies data
    rating_counts = ratings.groupby(["movieId", "rating"], as_index = False).count().rename({"userId": "count"}, axis = 1).pivot(index="movieId", columns = "rating", values = "count")
    rating_counts.columns = ['rating_' + str(col) for col in rating_counts.columns]
    movies_ratings_df = pd.merge(movies_df, rating_counts, how="left", left_on="kaggle_id", right_index = True)
    movies_ratings_df[rating_counts.columns] = movies_ratings_df[rating_counts.columns].fillna(0)
```



3. **Load**: after the data is ready we transfered it into it's final destination, a **PostgreSQL** database.  This was done with Python directly by using SQLAlchemy.


```

Create database and load merged, clean movies dataset


```
    db_string = f"postgres://postgres:{db_password}@127.0.0.1:5432/movie_data"
    engine = create_engine(db_string)
    movies_df.to_sql(name='movies', con=engine, if_exists='replace')
    
    rows_imported = 0
    start_time = time.time()
```


Load ratings.csv file to database


```
    start_time = time.time()
    for data in pd.read_csv(f'{file_dir}/ratings.csv', chunksize=1000000):
        print(f'importing rows {rows_imported} to {rows_imported + len(data)}...', end='')
        data.to_sql(name='ratings', con=engine, if_exists='append')
        rows_imported += len(data)

        # add elapsed time to final print out
        print(f'Done. {time.time() - start_time} total seconds elapsed')
```

<img src="https://github.com/NataliaVelasquez18/Movies_ETL/blob/main/Resources/movies_query.png" width="350" height="250" />
