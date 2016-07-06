# Yelp Maps

### 1. Introduction
In this project, we will create a visualization of restaurant ratings using machine learning and the [Yelp academic dataset]. In this visualization, Berkeley is segmented into regions, where each region is shaded by the predicted rating of the closest restaurant (yellow is 5 stars, blue is 1 star). Specifically, the visualization we will be constructing is a Voronoi diagram.

In the map above, each dot represents a restaurant. The color of the dot is determined by the restaurant's location. For example, Northside restaurants are colored blue. The user that generated this map has a strong preference for Southside restaurants, so you can see that the predicted ratings for Southside restaurants are higher than restaurants anywhere else.

This project uses concepts from Sections 2.1, 2.2, 2.3, and 2.4.3 of [Composing Programs]. It also introduces techniques and concepts from machine learning, a growing field at the intersection of computer science and statistics that analyzes data to find patterns and improve performance.

### 2. Project Hierarchy

##### Data Abstraction
Picking proper data structures for fast data access and computation.


##### Unsupervised Learning
Restaurants tend to appear in clusters (e.g. Southside restaurants, Gourmet Ghetto). In this phase, we will devise a way to group together restaurants that are close to each other.

The __k-means algorithm__ is a method for discovering the centers of clusters. It is called an unsupervised learning method because the algorithm is not told what the correct clusters are; it must infer the clusters from the data alone.

The k-means algorithm finds `k` centroids within a dataset that each correspond to a cluster of inputs. To do so, k-means begins by choosing `k` centroids at random, then alternates between the following two steps:

- Group the restaurants into clusters, where each cluster contains all restaurants that are closest to the same centroid.
- Compute a new centroid (average position) for each new cluster.

This [visualization] is a good way to understand how the algorithm works.



#### Supervised Learning
In this phase, we will predict what rating a user would give for a restaurant. We will implement a supervised learning algorithm that attempts to generalize from examples for which the correct rating is known, which are all of the restaurants that the user has already rated. By analyzing a user's past ratings, we can then try to predict what rating the user might give to a new restaurant.

To predict ratings, we will implement __simple least-squares linear regression__, a widely used statistical method that approximates a relationship between some input feature (such as price) and an output value (the rating) with a line. The algorithm takes a sequence of input-output pairs and computes the slope and intercept of the line that minimizes the mean of the squared difference between the line and the outputs.



### 3. Files

Files in this project:

* `abstractions.py`: Data abstractions used in the project
* `recommend.py`: Machine learning algorithms and data processing
* `utils.py`: Utility functions for data processing
* `ucb.py`: Utility functions for CS 61A
* `data`: A directory of Yelp users, restaurants, and reviews
* `users`: A directory of user files
* `visualize`: A directory of tools for drawing the final visualization


### 4. Running (GUI) - Predicting your own ratings

You can use your project to predict your own ratings too!

1. In the `users` directory, you'll see a couple of `.dat` files. Copy one of them and rename the new file to `yourname.dat` (for example, `john.dat`).

2. In the new file (e.g. `john.dat`), you'll see something like the following:
    ```python
        make_user(
	        'John DoeNero',     # name
		        [                   # reviews
			            make_review('Jasmine Thai', 4.0),
				                ...
						        ]
							    ```
							        Replace the second line with your name (as a string).

3. Replace the existing reviews with reviews of your own! You can get a list of Berkeley restaurants with the following command:
    ```sh
        $ python3 recommend.py -r
	    ```

4. Use `recommend.py` to predict ratings for you:
    ```sh
        $ python3 recommend.py -u john -k 2 -p -q Sandwiches
	    ```
	        (Replace `john` with your name.) Play around with the number of clusters (the `-k` option) and try different queries (with the `-q` option)!

### 5. Class Project Site
[here]

[here]: <http://61a-su15-website.github.io/proj/maps/>
[Yelp academic dataset]: <https://www.yelp.com/dataset_challenge>
[Composing Programs]: <http://composingprograms.com/>
[visualization]: <http://tech.nitoyon.com/en/blog/2013/11/07/k-means/>