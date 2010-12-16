.. _assignmentoperators:

Assignment operators
====================

In R you can perform assignment in 3 different ways using ``<-``, ``=`` and ``<<-`` operators. A simple example demonstrating how you can use them, 

.. code-block:: r

	x = value
	x <- value
	x <<- value
	value -> x
	value ->> x

Note ``<<-`` assigns ``x`` to ``value`` in the global context. The operators ``<<- or ->>`` cause a search to made through the environment for an existing definition of the variable being assigned. If such a variable is found (and its binding is not locked) then its value is redefined, otherwise assignment takes place in the global environment.

.. code-block:: r

	> a <- c(1,2,10)
	> a
	[1]  1  2 10
	> b =  c(13,7,9)
	> b
	[1] 13  7  9
	> b + a -> c
	> c
	[1] 14  9 19

The difference between ``=`` and ``<- or ->`` can be clearly observed  when they are used inside the function. The operator ``<- or ->`` can be used anywhere, whereas the operator ``=`` is only allowed at the top level (e.g., in the complete expression typed at the command prompt) or as one of the subexpressions in a braced list of expressions. In addition there also differences in scope. For instance in following example x is not found when we use ``=`` 

.. code-block:: r

	> median(x = 1:10)
	[1] 5.5
	> x
	Error: object 'x' not found
	> median(x <- 1:10)
	[1] 5.5
	> x
	 [1]  1  2  3  4  5  6  7  8  9 10
	> median(y = 1:10)
	Error in median(y = 1:10) : unused argument(s) (y = 1:10)

It is important to note as best practise some people just ignore using ``=`` and prefer to use ``<- or ->`` which makes their R code compatible with S/S-Plus.
