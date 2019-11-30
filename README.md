## Designing a Scalable Movie Recommender System with Apache Spark and Google Colab

### Summary

Semester Project for Télécom Paris MS Big Data's *Big Data Mining* (SD 701) Course. The goal of this project is to extract insights from a large dataset with the help of Big Data frameworks (Spark, Hadoop) and machine learning techniques (e.g. classification, collaborative filtering, clustering, frequent pattern mining) seen during the semester course.

### Implementation

As our working environment, we used Google Colab to run our Apache Spark implementation:

[View Jupyter Notebook with MovieLens Recommender System Implementation](https://nbviewer.jupyter.org/github/SJD1882/Big-Data-Recommender-Systems/blob/master/notebooks/MovieLens27M-ALS-Recommender-System.ipynb)

### Data

I chose [University of Minnesota's MovieLens Dataset](https://grouplens.org/datasets/movielens/), widely used in the machine learning community as a benchmark for implementing and improving state-of-the-art recommender systems. I specifically chose one of the latest iterations of MovieLens which was [last updated](https://grouplens.org/datasets/movielens/latest/) in September 2018. It contains:

- 27,000,000 user ratings from 280,000 users (between 1995 and 2018)
- 58,000 rated movies
- Table for linking MovieLens identifiers with IMDb and TMDb identifiers

### Models

- *Popularity-Based Model* where we only recommend the highest rated movies
- *Colaborative Filtering* using Latent Factor Models (with Spark ML's `ALS` Model)

### Results

At first glance, our results with our first approach model-based collaborative filtering are mixed. The RMSE on the testing set is 0.0823 which is close to a benchmark result seen in this [arXiv research paper](https://arxiv.org/abs/1606.07659) on a different MovieLens dataset (with 20 million ratings). However, precision and NDCG (for the first 20 recommended items) for CF-ALS on the testing set are a low 0.0003\% and 0.0002\% respectively. Our popularity model outperforms CF-ALS significantly on both those metrics. Finally as shown with catalog coverage, both models struggle to recommend most of the available pool of movies to users.

One reason why our collaborative filtering model underperforms on precision and NDCG is that accuracy-based metrics are biased in favor of popular items. Our catalog coverage showed that CF-ALS produced more diverse recommendations on average then the popularity-based model. But as the vast majority of movies are almost never rated (known as the long tail of items), CF-ALS has much weaker accuracy as it generates more diverse but less relevant item recommendations (which might be more appealing than recommending the same popular movies).

One reason might be that the missing entries (here unrated movies) in our ratings interaction matrix are actually Missing Not At Random (MNAR): as users can watch any movie they want, the probability of a rating being missing is not at random. Thus, the ratings distribution on the highest rated movies are different from the ratings distribution of movies on the long tail (vast majority). It might be more ideal to compute accuracy metrics separately for the most popular movies and the rest of the movie catalog.