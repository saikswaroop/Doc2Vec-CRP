# Doc2Vec-CRP

Clusters Vectors based on similarity.

Now let’s explain CRP. Imagine you go to a restaurant. There are already n tables with different number of peoples. There is also an empty table. CRP has a hyperparamter r > 0, which can be regarded as the “imagined” number of people on the empty table. You go to one of the (n+1) tables with probability proportional to existing number of people on the table. (For the empty table, the number is r). If you go to one of the n existing tables, you are done. If you decide to sit down at the empty table, the restaurant will automatically create a new empty table. In that case, the next customer comes in will choose from (n+2) tables (including the new empty table).

Inspired by CRP, I tried the following variations of CRP to include the similarity factor. Common setup is the following: we are given M vectors to be clustered. We maintain two things: cluster sum (not centroid!), and vectors in clusters. We iterate through vectors. For current vector V, suppose we have n clusters already. Now we find the cluster C whose cluster sum is most similar to current vector. Call this score sim(V, C).

If sim(V, C) > 1/(1 + n), goes to cluster C. Otherwise with probability 1/(1+n) it creates a new cluster and with probability n/(1+n) it goes to C.

In any of the two variants, if v goes to a cluster, we update cluster sum and cluster membership.

There is one distinct difference to traditional CRP: if we don’t go to empty table, we deterministically go to the “most similar” table.

In practice, we find these variants create similar results.


