# Movies-ETL

## Project Overview
The purpose of this project was to demonstrate the data pipeline process, ETL (Extract, Transform, Load), on movie datasets. Given extracted data with different file types, Python and Pandas were used to perform data wrangling. The project also includes how datasets are loaded to PostgreSQL.

### Resources
- Data Source:
    - [wikipedia-movies.json](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/Data%20Source/wikipedia-movies.json) - Wikipedia data that contains information on movies released since 1990
    - [movies_metadata.csv](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/Data%20Source/movies_metadata.csv) from https://www.kaggle.com/rounakbanik/the-movies-dataset
    - [ratings.csv](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/Data%20Source/ratings.csv.zip) from https://www.kaggle.com/rounakbanik/the-movies-dataset
- Language: Python 3.7.10
    - Dependencies:
        - Numpy, Pandas, JSON, re, sqlalchemy, psycopg2, time
- Software: Jupyter Notebook 6.3.0, PostgreSQL 12.7, pgAdmin 4 v5.4
- Refer to [ETL_create_database.ipynb](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/ETL_create_database.ipynb) for complete code

## Method
The project was divided into four parts with the objective of testing each step first to ensure script is functional, before combining all codes into one file.

### 1. Create Function to Read Data Files
#### *Refer to: [ETL_function_test.ipynb](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/ETL_function_test.ipynb)*
A function was created to read the three data files from a specified directory. Each DataFrame was checked by displaying the table to confirm that the function works.

### 2. Extract and Transform Wikipedia Data
#### *Refer to: [ETL_clean_wiki_movies.ipynb](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/ETL_clean_wiki_movies.ipynb)*
The transforming of the Wikipedia data starts with the creation of a function that would clean the columns. The function created in step 1 was modified by further cleaning the data through dropping rows with null values as well as columns that are not needed. Columns were converted to the appropriate data type and was transformed using **list comprehension, lambda function, and regular expression**.

### 3. Extract and Transform Kaggle Data
#### *Refer to: [ETL_clean_kaggle_data.ipynb](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/ETL_clean_kaggle_data.ipynb)*
The code from step 2 was modified by adding the Kaggle metadata right after the cleaning of the Wikipedia data. Same with step 2, a column not needed was dropped and data types were converted where it was appropriate. The two DataFrames were then merged and missing values were filled in by creating a function. Only columns needed were selected and renamed for a much neater DataFrame (movies_df). For the ratings, a pivot was created before merging with movies_df.

### 4. Create Movie Database
#### *Refer to: [ETL_create_database.ipynb](https://github.com/samanthajpv/Movies-ETL/blob/3401ed6098b10c54cea67b7aa4b3f9fa47e110ba/ETL_create_database.ipynb)*
A local server connection string was used to create the database engine. ```.to_sql``` was used to import the clean DataFrame (movies_df) and the ratings to PostgreSQL. The time method showed the time elapsed in importing the ratings. Using this method in other codes can also be beneficial in measuring script efficiency. With the clean data, it will now be easier to perform analysis.

## Reference
(1) Trilogy Education Services. (2021, August). *Module 8 Challenge*. https://courses.bootcampspot.com/courses/626/assignments/13398?module_item_id=212820
