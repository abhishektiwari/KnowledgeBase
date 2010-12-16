.. _rvectorfactormatrixarraylistdataframe:

Vector, Factor, Matrix, Array, List or Data.frame
=================================================

(`adopted from <http://en.wikibooks.org/wiki/R_Programming/Introduction>`_)

Vectors are the simplest R objects. Factors are similar to vectors but with a predetermined set of levels. A matrix is like a vector but with a specific instruction for the layout such that it looks like a matrix. Arrays are similar to matrix but can have more than 2 dimensions. A list is a vector of R objects. A dataframe is like a matrix but does not assume that all columns have the same type. A dataframe is a list of variables/vectors of the same length. Classes define how objects of a certain type look like. Classes are attached to object as an attribute. All R objects have a class, a type and a dimension.



.. code-block:: r

							______ factor, factor(v1, ordered = T)
						       |
						       |______ matrix, cbind(v1, v2, ...), rbind(v1, v2, ...)
						       |
			R objects-----  Vectors--------|______ array, array(v1,dim=c(3,2,4))
					(v1, v2, ...)  |
						       |______ data.frame, data.frame(v1, v2, ...)
						       |
						       |______ list, list(name1 =v1, name2 = v2, ...)



Vectors
-------

You can create a vector using the ``c()`` function which concatenates some elements. You can create a sequence using the : symbol or the ``seq()`` function. For instance 1:5 gives all the number between 1 and 5. The ``seq()`` let you specify the interval between each number. You can also repeat a pattern using the ``rep()`` function. You can also create a numeric vector of missing values using ``numeric()``, a character vector of missing values using ``character()`` and a logical vector of missing values (ie FALSE) using ``logical()``

.. code-block:: r

	> c(1,2,3,4,5)
	[1] 1 2 3 4 5
	> c("a","b","c","d","e")
	[1] "a" "b" "c" "d" "e"
	> c(T,F,T,F)
	[1]  TRUE FALSE  TRUE FALSE
	> 1:5
	[1] 1 2 3 4 5
	> 5:1
	[1] 5 4 3 2 1
	> seq(1,5)
	[1] 1 2 3 4 5
	> seq(1,5,step=.5)
	[1] 1 2 3 4 5
	> seq(1,5,by=.5)
	[1] 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0
	> rep(1,5)
	[1] 1 1 1 1 1
	> rep(1:2,5)
	 [1] 1 2 1 2 1 2 1 2 1 2
	> numeric(5)
	[1] 0 0 0 0 0
	> logical(5)
	[1] FALSE FALSE FALSE FALSE FALSE
	> character(5)
	[1] "" "" "" "" ""

The ``length()`` computes the length of a vector.

.. code-block:: r

	x <- seq(1,5,by=.5)                # Create a sequence of number
	x                                  # Display this object
	[1] 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0
	> length(x)                        # Get length of object x
	[1] 9

``last()`` (sfsmisc) returns the last element of a vector.

Factors
-------

``factor()`` transform a vector into a factor. A factor can also be ordered with the option ``ordered=T`` or the function ``ordered()``. ``levels()`` returns the levels of a factor. ``gl()`` generates factors. n is the number of levels, k the number of repetition of each factor and length the total length of the factor. labels is optional and gives labels to each level.

.. code-block:: r
 
	> factor(c("yes","no","yes","don't","don't","no","don't","no","no"))
	[1] yes   no    yes   don't don't no    don't no    no   
	Levels: don't no yes
	> 
	> factor(c("yes","no","yes","don't","don't","no","don't","no","no"), ordered = T)
	[1] yes   no    yes   don't don't no    don't no    no   
	Levels: don't < no < yes
	> 
	> ordered(c("yes","no","yes","don't","don't","no","don't","no","no"))
	[1] yes   no    yes   don't don't no    don't no    no   
	Levels: don't < no < yes
	>
	>  gl(n=2, k=2, length=10, labels = c("Male", "Female")) # generate factor levels
	[1] Male   Male   Female Female Male   Male   Female Female Male   Male  
	Levels: Male Female

Matrix
------

If you want to create a new matrix, one way is to use the ``matrix()`` function. You have to enter a vector of data, the number of rows and/or columns and finally you can specify if you want R to read your vector by row or by column (the default option). Here are two examples.

.. code-block:: r

	> matrix(data = NA, nrow = 5, ncol = 5, byrow = T)
	     [,1] [,2] [,3] [,4] [,5]
	[1,]   NA   NA   NA   NA   NA
	[2,]   NA   NA   NA   NA   NA
	[3,]   NA   NA   NA   NA   NA
	[4,]   NA   NA   NA   NA   NA
	[5,]   NA   NA   NA   NA   NA
	> matrix(data = 1:15, nrow = 5, ncol = 5, byrow = T)
	     [,1] [,2] [,3] [,4] [,5]
	[1,]    1    2    3    4    5
	[2,]    6    7    8    9   10
	[3,]   11   12   13   14   15
	[4,]    1    2    3    4    5
	[5,]    6    7    8    9   10

Functions ``cbind()`` and ``rbind()`` combine vectors into matrices in a column by column or row by row mode:

.. code-block:: r

	> v1 <- 1:5
	> v2 <- 5:1
	> v2
	[1] 5 4 3 2 1
	> cbind(v1,v2)
	     v1 v2
	[1,]  1  5
	[2,]  2  4
	[3,]  3  3
	[4,]  4  2
	[5,]  5  1

	> rbind(v1,v2)
	   [,1] [,2] [,3] [,4] [,5]
	v1    1    2    3    4    5
	v2    5    4    3    2    1

The dimension of a matrix can be obtained using the ``dim()`` function. Alternatively ``nrow()`` and ``ncol()`` returns the number of rows and columns in a matrix:

.. code-block:: r

	> dim(X)
	[1] 5 5
	> nrow(X)
	[1] 5
	> ncol(X)
	[1] 5
	Function t() transposes a matrix:
	> X<-matrix(data = 1:15, nrow = 5, ncol = 5, byrow = T)
	> t(X)
	     [,1] [,2] [,3] [,4] [,5]
	[1,]    1    6   11    1    6
	[2,]    2    7   12    2    7
	[3,]    3    8   13    3    8
	[4,]    4    9   14    4    9
	[5,]    5   10   15    5   10

Data Frames
-----------

A dataframe has been referred to as "a list of variables/vectors of the same length". In the following example, a dataframe of two vectors is created, each of five elements. The first vector, v1, is compose of a sequence of the integers 1 through 5. A second vector, v2, is composed of five logical values drawn of type T and F. The dataframe is then created, composed of the vectors.

.. code-block:: r

	> v1 = 1:5
	> v2 = c(T,T,F,F,T)
	> df = data.frame(v1,v2)
	> print(df)
	  v1    v2
	1  1  TRUE
	2  2  TRUE
	3  3 FALSE
	4  4 FALSE
	5  5  TRUE

The dataframe may be created directly. In the following code, the dataframe is created - naming each vector composing the dataframe as part of the argument list.

.. code-block:: r

	> df = data.frame(foo=1:5,bar=c(T,T,F,F,T))
	> print(df)
	  foo   bar
	1   1  TRUE
	2   2  TRUE
	3   3 FALSE
	4   4 FALSE
	5   5  TRUE

Arrays
------

An array is composed of n dimensions where each dimension is a vector of R objects of the same type. An array of one dimension of one element may be constructed as follows.

.. code-block:: r

	> x = array(c(T,F),dim=c(1))
	> print(x)
	[1] TRUE

The array x was created with a single dimension (``dim=c(1)``) drawn from the vector of possible values ``c(T,F)``. A similar array, y, can be created with a single dimension and two values.

.. code-block:: r

	> y = array(c(T,F),dim=c(2))
	> print(y)
	[1]  TRUE FALSE

A three dimensional array - 3 by 3 by 3 - may be created as follows.

.. code-block:: r

	> z = array(1:27,dim=c(3,3,3))
	> dim(z)
	[1] 3 3 3
	> print(z)
	, , 1

	     [,1] [,2] [,3]
	[1,]    1    4    7
	[2,]    2    5    8
	[3,]    3    6    9

	, , 2

	     [,1] [,2] [,3]
	[1,]   10   13   16
	[2,]   11   14   17
	[3,]   12   15   18

	, , 3

	     [,1] [,2] [,3]
	[1,]   19   22   25
	[2,]   20   23   26
	[3,]   21   24   27

R arrays are accessed in a manner similar to arrays in other languages: by integer index, starting at 1 (not 0). The following code shows how the third dimension of the 3 by 3 by 3 array can be accessed. The third dimension is a 3 by 3 array.

.. code-block:: r

	> z[,,3]
	     [,1] [,2] [,3]
	[1,]   19   22   25
	[2,]   20   23   26
	[3,]   21   24   27

Specifying two of the three dimensions returns an array on one dimension.

.. code-block:: r

	> z[,3,3]
	[1] 25 26 27

Specifying three of three dimension returns an element of the 3 by 3 by 3 array.

.. code-block:: r

	> z[3,3,3]
	[1] 27

More complex partitioning of array may be had.

.. code-block:: r

	> z[,c(2,3),c(2,3)]
	, , 1

	     [,1] [,2]
	[1,]   13   16
	[2,]   14   17
	[3,]   15   18

	, , 2

	     [,1] [,2]
	[1,]   22   25
	[2,]   23   26
	[3,]   24   27

Arrays need not be symmetric across all dimensions. The following code creates a pair of 3 by 3 arrays.

.. code-block:: r

	> w = array(1:18,dim=c(3,3,2))
	> print(w)
	, , 1

	     [,1] [,2] [,3]
	[1,]    1    4    7
	[2,]    2    5    8
	[3,]    3    6    9

	, , 2

	     [,1] [,2] [,3]
	[1,]   10   13   16
	[2,]   11   14   17
	[3,]   12   15   18

Objects of the vectors composing the array must be of the same type, but they need not be numbers.

.. code-block:: r

	> u = array(c(T,F),dim=c(3,3,2))
	> print(u)
	, , 1

	      [,1]  [,2]  [,3]
	[1,]  TRUE FALSE  TRUE
	[2,] FALSE  TRUE FALSE
	[3,]  TRUE FALSE  TRUE

	, , 2

	      [,1]  [,2]  [,3]
	[1,] FALSE  TRUE FALSE
	[2,]  TRUE FALSE  TRUE
	[3,] FALSE  TRUE FALSE

Lists
-----

An R list is an object consisting of an ordered collection of objects known as its components. Function ``list()`` transforms R-objects into list,

.. code-block:: r

	lst <- list(name1 = object1, name2 = object2, name3 = object3,  ..., name_m = object_m)


Components can accessed as,

.. code-block:: r

	${lst$name_m}, lst[["name_m"]] or lst[[m]]. 

To access elements inside the components, 

.. code-block:: r
	
	lst[[m]][n]

Similarly, function ``unlist()`` transform a list into a vector

.. code-block:: r
	
	vec <- unlist(lst)
