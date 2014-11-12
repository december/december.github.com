---
layout: post
category: Matlab
tags: FEMA data generation
description: A data generater for FEMA.
---

### Application

  * Generate core tensor with specified parameters.
  * Generate projection matrix with specified parameters.
  * Generate a tensor describing a behavior model with specified parmeters.
  * Decompose a tensor and produce a core tensor with projection matrixes.
  * Calculate the margin of error of core tensors or projection matrixes.
  * Record the time spent in generating various datas.

### Tool Used

  * **MatLab**
  * **Tensor Toolbox**
	
### makecore.m

  * **Function** : Generate a sparse tensor as the core tensor with specified parameters.
  * **Usage** : function [y] = makecore(d, mx, mn, n, rate ,noise);
  * **Parameters** :  

  		% d : the number of dimension
		% mx : the max value of diagonal elements
		% mn : the min value of diagonal elements
		% n : the edge length of the cube core
		% rate : the rate of non-zero nondiagonal elements
		% noise : the max possible value of nondiagonal elements

  * **Return** : y : the core tensor to be generated.
  * **Example** : 

		y = makecore(3, 1000, 100, 10, 0.01, 3);

		Elapsed time is 1.846068 seconds.
		ans is a sparse tensor of size 10 x 10 x 10 with 20 nonzeros
   		1.0e+03 *
			( 1, 2, 8)    0.0021
			( 2,10, 9)    0.0001
			( 3, 5, 8)    0.0008
			( 6,10, 4)    0.0001
			( 7, 9, 7)    0.0003
			( 9, 2, 7)    0.0025
			(10, 5,10)    0.0021
			(10, 8, 7)    0.0010
			(10,10, 1)    0.0029
			(10,10, 2)    0.0001
			( 1, 1, 1)    1.0000
			( 2, 2, 2)    0.9000
			( 3, 3, 3)    0.8000
			( 4, 4, 4)    0.7000
			( 5, 5, 5)    0.6000
			( 6, 6, 6)    0.5000
			( 7, 7, 7)    0.4000
			( 8, 8, 8)    0.3000
			( 9, 9, 9)    0.2000
			(10,10,10)    0.1000


### makepm.m

  * **Function** : Generate projection matrix with specified parameters and normalize it by column.
  * **Usage** : function [A] = makepm(l, s, t, dr, ndr);
  * **Parameters** :  

  		% l : the length of long edge
		% s : the length of short edge
		% t : the standard value of diagonal elements
		% dr : the random range of diagonal elements
		% ndr : the random range of nondiagonal elements

  * **Return** : A : the projection matrix to be generated
  * **Example** :

  		makepm(10, 3, 10, 1, 1);

		Elapsed time is 0.100353 seconds.

		ans =

    		0.5279    0.0159    0.0436
    		0.4699    0.0391    0.0148
    		0.5253    0.0377    0.0293
    		0.4689    0.0094    0.0405
    		0.0092    0.6251    0.0517
    		0.0242    0.5584    0.0556
    		0.0220    0.5408    0.0317
    		0.0319    0.0196    0.5511
    		0.0351    0.0337    0.5934
    		0.0373    0.0129    0.5769
		

### tucker.m

  * **Function** : Generate a tensor describing a behavior model with specified parmeters using makecore.m and makepm.m. 
  * **Usage** : function [x, y, A1, A2, A3] = tucker(d, lg, lgc, mx, mn, t, dr, ndr, rate, noise);
  * **Parameters** :  

		% d   : the number of dimension
		% lg  : length of the whole tensor
		% lgc : length of the core tensor
		% mx  : the max value of diagonal elements in core tensor
		% mn  : the min value of diagonal elements in core tensor
		% t   : the standard value of diagonal elements in projection matrix
		% dr  : the random range of diagonal elements in projection matrix
		% ndr : the random range of nondiagonal elements in projection matrix
		% rate : the rate of non-zero nondiagonal elements in core tensor
		% noise : the max possible value of nondiagonal elements in core tensor

  * **Return** : 

  		x : the tensor describing a behavior model
		y : the core tensor of x
		A1 : the first projection matrix of x
		A2 : the second projection matrix of x
		A3 : the third projection matrix of x

  * **Example** :
  
		[x, y, A1, A2, A3] = tucker(3, 12, 3, 1000, 100, 10, 1, 0, 0.01, 3);

### ayz.m

  * A script to generate tensors using tucker.m and decompose tensors using tuckerals and calculate the error of core tensors and projection matrixes individually.

### TO DO LIST

  * Read data from files and write result into files.
  * Practice FEMA and compare the efficiency and error.
  * Data visualization.

