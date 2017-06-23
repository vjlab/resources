# Tree Computation - IQ-Tree, FastTree, RAxML and BEAST

### IQTree
 - ML-based. 
 - Not terribly fast. It *could* be faster than RAxML; I've never really tested it. 

### FastTree
 - Fast, as you may have picked up from the name. Typically terminates within minutes, even with thousands of sequences.
 - Computes only one tree, so the results of FastTree are questionable not so much because of the accuracy of the tree, but because it doesn't give a way to assess the quality of the result (e.g. by likelihood or empirical support).
