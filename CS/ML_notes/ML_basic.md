# Decision Tree

1. Entropy: The randomness of data.
        
      H(X) = -∑P(x)•log(P(x))
    
2. Information Gain: How much information we can get from a partition of data.
    
      IG(d, D) = H(t,D) - rem(d, D)
      rem(d, D) = ∑ len(d) / len(D) * H(t, D)
    
3. ID3 Alogoritm: Attempt to creat shallowest tree that fits the data

      Make each node according to the IG value, and build recursively and depth first.
        
4. Information Gain Ratio：

      GR(d, D) = IG(d, D)/H(d, D)
        
5. Gini Index: Measure impurity

      Gini(d, D) = 1 - ∑P(d)<sup>2</sup>
      
6. Advantages

    * Relatively easy to interpret the generated tree.

    * Easy to use and understand.

    * Compared to other methods, DT requires less effort in data
    preparation.

    * Contains an internal method for attribute selection.

    * Missing values dose not have a huge impact on building the decision
    tree.
7. Disadvantages

    * A small change in the data may cause big impact on the structure of
    the developed tree.
    
    * Relatively, requires heavy mathematical calculations and memory in
    training.
    
    * Information gain is a “heuristic” – does not guarantee optimality. 
    
# KNN

1. Disadvantages:

    * Slow in classification – requires high processing
    
    * Requires memory to store all previous instances
    
2. Advantages:
    
    * Dynamic – you can easily update the model by add
new instanceses

# K-Means

1. Pre-processing:

    * Normalize the data

    * Eliminate outliers

2. Post-processing:

    * Eliminate small clusters that may represent outliers
    
    * Split ‘loose’ clusters, i.e., clusters with relatively high SSE
       
    * Merge clusters that are ‘close’ and that have relatively low SSE

    * Can use these steps during the clustering process: ISODATA
    
3. Limitation:

    * K-means has problems when clusters are of differing:
    
        1. Sizes
    
        2. Densities
    
        3. Non-globular shapes
        
    * K-means has problems when the data contains outliers

# Hierarchical Clustering
        
1. Two common way to build:

     1. Merge clusters from each single point
     2. Seperate from a single cluster
    
2. Inter-cluster Similarity Measure

      * Min: measuring shortest distance betweent two cluster
           * Sensitive to noise and outliers
      * Max: measuring longest distance betweent two cluster
           * Less sensitive to noise and outliers
           * Tend to split large cluster, biased toward globular cluster
      * Average: measuring average distance between two cluster
           * Less susceptible to noise and outliers
           * Biased toward globular cluster
      * Ward’s Method: measuring increased sequared errors
           * Less susceptible to noise and outliers
           * Biased towards globular clusters
           * Can used to initialize K-Means
# DBSCAN

1. Advantages:

    * Resistant to noise
    * Handles clusters of different size shapes
2. Disadvantages:

    * Can't handle high dimentional data
    * Can't handle clusters with varing density

# Cluster Evaluation
