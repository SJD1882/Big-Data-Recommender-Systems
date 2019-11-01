## Designing a Scalable Movie Recommender System with Apache Spark and Google Colab

#### Summary

Semester Project for Télécom Paris MS Big Data's *Big Data Mining* (SD 701) Course.

The goal of this project is to extract insights from a large dataset with the help of Big Data frameworks (Spark, Hadoop) and machine learning techniques (e.g. classification, collaborative filtering, clustering, frequent pattern mining) seen during the semester course.

#### Google Colab Notebooks

As our working environment, we used Google Colab to run our Apache Spark.

- View `Exploratory Data Analysis` with Notebook Viewer (To Be Added)
- View `Model Training & Results` with Notebook Viewer (To Be Added)

#### Data

I chose [University of Minnesota's MovieLens Dataset](https://grouplens.org/datasets/movielens/), widely used in the machine learning community as a benchmark for implementing and improving state-of-the-art recommender systems. I specifically chose one of the latest iterations of MovieLens which was [last updated](https://grouplens.org/datasets/movielens/latest/) in September 2018. It contains:

- 27,000,000 user ratings from 280,000 users (between 1995 and 2018)
- 58,000 rated movies
- 1,100 genome tags per movie (which provide metadata)
- Table for linking MovieLens identifiers with IMDb and TMDb identifiers

#### Models

- *Popularity-Based Model* where we only recommend the highest rated movies
- *Colaborative Filtering* using Latent Factor Models (with `Spark ML`)

#### Results

*(Work In Progress)*