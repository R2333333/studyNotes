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

    • Relatively easy to interpret the generated tree.

    • Easy to use and understand.

    • Compared to other methods, DT requires less effort in data
    preparation.

    • Contains an internal method for attribute selection.

    • Missing values dose not have a huge impact on building the decision
    tree.
7. Disadvantages

    • A small change in the data may cause big impact on the structure of
    the developed tree.
    
    • Relatively, requires heavy mathematical calculations and memory in
    training.
    
    • Information gain is a “heuristic” – does not guarantee optimality. 
    
# KNN

1. Disadvantages:

    • Slow in classification – requires high processing
    
    • Requires memory to store all previous instances
    
2. Advantages:
    
    • Dynamic – you can easily update the model by add
new instanceses

