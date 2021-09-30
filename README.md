# Extract, Transform and Load Movies DataBase

In this week project, we gather data about **Movies** from different websites, combine them and then save them into a `SQL` database so it can be used as a dataset in a Hackathon. Also, we need to automatize the process of take in new data, so the people working in the Hackathon could be updated on a daily basis.

## Overview

In order to carry out this week project, we need to follow an Extraction, Transform and Load (ETL) process, where  the first step is to extract data about movies from *Wikipedia*, *Kaggle* and *MovieLens*.  The second step is to transform the datasets loaded as tables by cleaning them up and joining them together.  Finally,  importe the cleaned dataset into a  **SQL** database.  **Python**, specifically *jupyter notebook* is used in the three steps and **PostgreSQL** is used to load and save the database.

## Results:

We work with three different dataset: **Wikipedia dat**, **Kaggle metadata** and **MovieLens rating data** to create a Movie Database that will have two tables: `movies` and `ratings` and that will be stored in PostgreSQL.

### 1. ETL Function to Read the Three Data Files:

The function to read the three files is written in jupyter notebook.  We need to use `json.load()` function to convert the Wikipedia JSON data to raw data, and then convert it into a Pandas DataFrame. Regarding, the Kaggle and MovieLens files, they are reading directly and convert them into Pandas DataFrames by using the function `read_csv` of the Pandas module.  An overview of the three dataframes is shown below.

![wiki_1](https://raw.githubusercontent.com/LeidyDoradoM/MoviesETL_Challenge/main/Resources/df_wiki_del1.png)

![kaggle_1](https://raw.githubusercontent.com/LeidyDoradoM/MoviesETL_Challenge/main/Resources/df_kaggle_del1.png)

![ratings_1](https://raw.githubusercontent.com/LeidyDoradoM/MoviesETL_Challenge/main/Resources/df_ratings_del1.png)
Figure 1. Overview of the three datasets

### 2. Extract and Transform the Wikipedia Data:

Once the datasets are loaded as DataFrames, we need to clean and transform them so we can merge them and have a tidy, organized and more reliable dataset in which further analysis can be performed.  The Wikipedia dataset is specially messy since different pages are edited by different people, and different movies can have different columns.  Therefore, it is necessary to apply a consistent methodology where the data is inspected, a plan to remove/transform errors is designed and executed, is performed over and over until a clean and organized table of data, where every row is a single movie, is produced.
In general for this dataset, we keep only rows that correspond to movies, i.e. we remove series or tv shows. We also remove columns that have more than 90% of their values as `Null` values and remove alternative titles of the same movie keeping only one row per movie.  In addition, we convert and parse 4 different columns such every row has the same format and data type. These columns are: **Box office**, **Budget**, **Release date** and **Running time**.  Figure 2 shows and overview of the clean version for the Wikipedia dataset and its columns.


Figure 2. Overview of the Clean and Organized Wikipedia dataset

### 3. Extract and Transform the Kaggle Data:

The Kaggle data is more structured than the Wikipedia dataset, but still needs some cleaning, specially needs converting some strings to the correct data type. In this case we again follow the same methodology of inspecting the data, planning a process for removing errors or bad data and then execute it. We use the `to_numeric()` method from Pandas to convert columns in string as numeric data type. These columns are: **budget**, **id** and **popularity**.  We use also `to_datetime` for the **release_date** column.  Finally, the three datasets are merged such that the Wikipedia and Kaggle data are merged first as a `movie_df` dataframe and then, this new dataframe is merged with the MovieLens ratings table.  The new dataframe is called `movies_with_ratings_df`.
Figure 3 shows the two dataframes.


Figure 3. Overview of the merged Kaggle/Wikipedia dataframe and the merged version with MovieLens ratings

### 4. Create the Movie Database:

The four and last step is the importing of the dataframes as tables in a SQL database.  We import from Pandas-Python two dataframes: `movies_df` and `ratings` into PostgreSQL by using the method `to_sql`. Besides in PostgreSQL we verify that the two tables have the appropriate number of rows by making two queries that count the number of rows in each table.


Figure 4. Movies and ratings Queries and their results.
