# KNN #
10-fold CV KNN on BoW, TF-IDF, W2V &amp; TF-IDF weighted W2V (Brute force vs kd-tree)

## Amazon Fine Food Reviews Analysis ##

Data Source: https://www.kaggle.com/snap/amazon-fine-food-reviews

The Amazon Fine Food Reviews dataset consists of reviews of fine foods from Amazon.

Number of reviews: 568,454
Number of users: 256,059
Number of products: 74,258
Timespan: Oct 1999 - Oct 2012
Number of Attributes/Columns in data: 10

## Attribute Information: ##

    Id
    ProductId - unique identifier for the product
    UserId - unqiue identifier for the user
    ProfileName
    HelpfulnessNumerator - number of users who found the review helpful
    HelpfulnessDenominator - number of users who indicated whether they found the review helpful or not
    Score - rating between 1 and 5
    Time - timestamp for the review
    Summary - brief summary of the review
    Text - text of the review


## Objective: ##
To find accuracy of 10-fold cross validation KNN on vectorized input data, for each of the 4 featurizations, namely BoW, tf-IDF, W2V, tf-IDF weighted W2V. Running time comparison of Brute force vs kd-tree also need to be done.

## At a glance: ##
Random Sampling is done to reduce input data size and time based slicing to split into training and testing data. The accuracy percentage obtained by applying 10-fold cross validation KNN using 4 Featurizations viz. BoW, tf-idf, W2V, tf-idf W2V are compared. The time taken by brute force and kd-tree methods are plotted and analysed.

## Plots ##

![knn1](https://github.com/AdroitAnandAI/KNN/blob/master/Images/knn1.PNG)
![knn2](https://github.com/AdroitAnandAI/KNN/blob/master/Images/knn2.PNG)
![knn3](https://github.com/AdroitAnandAI/KNN/blob/master/Images/knn3.PNG)

## Observations ##
1. The Accuracy obtained using W2V featurization is slightly higher than BoW and tf-IDF methods, though not significantly higher.

2. When dimension is small (dim=5), the increase in running time of kd-tree knn is linear but the brute force algorithm is exponential. Hence, at lower dimensions, kd-tree performs better.

3. When dimension is high (dim=50), the increase in running time of kd-tree knn is exponential, but brute force algorithm is Comparatively linear. Hence, brute force is better when dimension is high.

4. Explanation of 2 & 3: It is known that kD-Trees don???t scale very well with high dimensionality. When d is not small, the time complexity of knn becomes, O (2??d*log n). When 2??d = n, then time complexity = O (n log n) which is more than brute force (O (n)). This
explains (3).

5. Even when d is small, time complexity of kd-tree would be O (log n) only when data is uniformly distributed. When data is not uniform, then kd-tree would move towards complexity of simple implementation, O (n) 

6. It has been noticed that the general rules given in (2) and (3) are not hard and fast. For the same number of datapoints, kd-tree is seen much efficient at very high dimensions.

## Timing Results: ##
(W2V dimension = 50) Brute Force = 2.16 seconds; kd-tree = 4.06 seconds <br/>
(W2V dimension = 500) Brute Force = 26.55 seconds; kd-tree = 25.14 seconds.

**Reason:** The performance may depend a lot on the characteristics of the data. For example, are the data points evenly distributed, clustered or otherwise arranged?

**Note:** What happens for kd-tree at high dimensions? To evaluate a query point at boundary, the circle drawn would intersect all adjoining regions. Thus, we have to look at all 2??d adjoining regions. when d = 20 then there are 1 million regions, which is huge! Thus, when dimensionality is 10K or 20K, then kd-tree is useless, as shown in the timing results.
