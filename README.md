This is a type of an algorithm that selects a cluster from a set of data points, removing unreliable outliers in the process: 
Iteratively, 

- it calculates the maximum likelihood estimators of the mean vector and the variance-covariance matrix of the data for the normal distribution, 

- then checks which points, considered outliers, are below a given treshold, 

- discards these outlier points and 

- recalcualtes again the maximum likelhood estimators but this time for the new reduced updated set of data points. 

- It terminates when no more outliers can be found.   


### INPUT:
We start with a data frame or data table or a matrix of data points E with rows looking like this: 

E[i, :] = [coord_1, coord_2, ..., coord_k] where i = 1, 2, ..., N

thus E has the structure of a (N rows) x (k columns) table/matrix. 

Each row  E[i, :] represents a data point in an k dimensional space. 

Set up a treshold sgm (umber of standard deviations you would like to include)


### ALGORITHM:
1. Initially X is simply equal to E but interpeted as a N x k matrix by R
   sgm is a treshold parameter we set ourselves which tells us hom many standard deviations we should be including in our cluster 

2. During each step: check if n == n_1 or not. If not:

   3. set n_1 to be the number of current data points in X (the number of rows of X)

   4. calculate Mean = n_1 x k matrix, each row is the same, and is equal to the coordinates of the centroid of the data 
      (the mean data   point of the sample) 

   5. calcualte Sigma_inv = the inverse of the k x k variance-covariance matrix of the data:
        Sigma_inv = ( t(X - M) * (X - M) / (n_1-1) )^(-1)

   6. for each point X[i,:] from X 
      calcualte the score t(X[i, :] - Mean[i, :]) * Sigma_inv * (X[i, :] - Mean[i, :]) 
      and check if it is less or equal to sgm. 

   7. remove all points from X whose score is > sgm 

   8. set n = number of rows of X (the number of points left, the ones whose score is  <= sgm)

   9. go back to step 2, the line which says " during each step: "
