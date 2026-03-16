# Movie Recommendation System

## Project Overview

This project builds a **movie recommendation system** using the MovieLens dataset. The goal is to recommend movies to users based on patterns in user ratings.

The model uses **item-based collaborative filtering with cosine similarity** to identify movies that are similar based on how users rated them. By analyzing rating patterns across users, the system can recommend movies that are likely to appeal to similar audiences.

This project demonstrates key data science concepts including:

* Data cleaning and preprocessing
* Exploratory data analysis (EDA)
* Feature engineering
* Collaborative filtering
* Recommendation system design

---

# Dataset

The project uses the **MovieLens dataset**, which contains movie ratings and metadata from thousands of users.

| File        | Description                                  |
| ----------- | -------------------------------------------- |
| movies.csv  | Movie titles and genres                      |
| ratings.csv | User ratings for movies                      |
| tags.csv    | User-generated tags describing movies        |
| links.csv   | External IDs linking movies to IMDb and TMDb |

The recommendation system primarily uses **ratings.csv and movies.csv**, since collaborative filtering relies on user rating behavior.

---

# Exploratory Data Analysis

Before building the recommendation model, the dataset was analyzed to better understand user behavior, movie popularity, and rating patterns.

---

## Rating Distribution

![Rating Distribution](images/rating_distribution.png)

The rating distribution shows clear spikes at **3.0, 3.5, 4.0, 4.5, and 5.0**.
This occurs because the MovieLens platform allows ratings in **half-star increments**, producing discrete rating clusters instead of a smooth distribution.

Most ratings fall between **3.0 and 4.5**, creating a **positive skew**.

### Interpretation

* Users are more likely to rate movies they enjoy.
* Extremely low ratings are relatively uncommon.
* Ratings cluster heavily in the **3–4.5 range**.

---

## Most Popular Movie

![Most Rated Movies](images/most_rated_movies.png)

The movie with the **highest number of ratings** was:

**The Shawshank Redemption (1994)**

Average rating: **4.4**

### Interpretation

* The most frequently rated movie is also highly rated.
* This suggests that **high popularity often aligns with strong audience approval**.

---

## Popularity vs Average Rating

![Popularity vs Rating](images/popularity_vs_rating.png)

A scatterplot comparing **number of ratings vs average rating** reveals several patterns:

* Most movies cluster between **3.0 and 4.2 average rating**
* Movies with very few ratings sometimes show extreme averages
* As rating counts increase, average ratings become more stable

### Interpretation

This pattern reflects **regression toward the mean**.

Movies with more ratings tend to have **more reliable averages**, because larger sample sizes reduce extreme values.

---

## Most Popular Genres

![Genre Popularity](images/genre_popularity.png)

The genres receiving the most ratings were:

1. **Drama**
2. **Action**
3. **Comedy**

There is roughly a **90% gap between Drama and Documentary** in total ratings.

### Interpretation

* Narrative-driven films dominate viewer engagement.
* Documentary films tend to attract smaller audiences.

---

## Highest Rated Genres

![Genre Ratings](images/genre_ratings.png)

The genre with the **highest average rating** was:

**Film-Noir**

Other observations:

* Drama ranked **fourth in average rating**
* Documentary ranked near the middle
* Horror had the **lowest average rating**

### Interpretation

Niche genres often receive higher ratings because they attract **dedicated audiences who already enjoy that style**.

More mainstream genres can be **more polarizing**, resulting in lower average ratings.

---

## Ratings Over Time

![Ratings Over Time](images/ratings_over_time.png)

Analysis of ratings by release year showed several trends:

* Older films tend to receive **higher average ratings**
* Recent films show slightly lower averages
* A small increase in ratings appeared after **2020**

### Interpretation

Possible explanations include:

* **Survivorship bias** – only well-regarded older movies remain widely watched
* **Classic film bias** – iconic films are rated more positively
* Increased streaming activity after 2020 may have increased engagement

Newer films may also have **fewer ratings**, which can affect their averages.

---

# Building the Recommendation System

The recommendation system uses **item-based collaborative filtering**.

Instead of recommending movies based on genres or descriptions, the system recommends movies based on **similar user rating behavior**.

### Step 1: Create Movie–User Matrix

A pivot table is created where:

* Rows represent **movies**
* Columns represent **users**
* Values represent **ratings**

Missing values are filled with **0**, since most users rate only a small subset of movies.

---

### Step 2: Convert to Sparse Matrix

Because the rating matrix contains many missing values, it is converted to a **sparse matrix** to improve computational efficiency.

---

### Step 3: Compute Cosine Similarity

Cosine similarity measures how similar two movies are based on their rating vectors.

Movies that receive **similar ratings from the same users** will have high similarity scores.

---

# Recommendation Results

The recommendation system successfully identifies movies that share similar rating patterns.

Example input:

```
The Shawshank Redemption (1994)
```

Recommended movies:

1. Pulp Fiction (1994)
2. Forrest Gump (1994)
3. The Silence of the Lambs (1991)
4. Schindler's List (1993)
5. The Usual Suspects (1995)

### Interpretation

The recommended movies are logically related because they share:

* Similar release periods
* Strong audience reception
* Overlapping viewer preferences

This confirms that the **collaborative filtering model is functioning correctly**.

---

# Key Takeaways

From the dataset analysis and modeling:

* Most movie ratings fall between **3.0 and 4.5**
* Popular movies often maintain **consistently strong ratings**
* **Drama dominates viewer engagement**
* **Film-Noir receives the highest average ratings**
* **Older films tend to receive higher ratings**
* Collaborative filtering successfully identifies **movies with similar audience preferences**

---

# Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

---

# Future Improvements

Possible improvements to this project include:

* Implementing **matrix factorization (SVD)** for improved recommendations
* Combining **content-based filtering with collaborative filtering**
* Building a **web interface for users**
* Adding **user-based recommendations**
* Expanding the dataset with additional metadata
