.. _rhadoop:

R Hadoop/MapReduce
==================

R Packages
----------


===================    =======    ============================================================================
    Packages            URL          Notes
===================    =======    ============================================================================
mapReduce               [#f1]_    Developed by Open Data Group, see the blog post [#f2]_
Hadoop InteractiVE      [#f3]_    R extension facilitating distributed computing via the MapReduce paradigm
RHIPE                   [#f4]_    R and Hadoop Integrated Processing Environment
===================    =======    ============================================================================


.. rubric:: URLs

.. [#f1] http://crantastic.org/packages/mapReduce
.. [#f2] http://opendatagroup.com/2009/09/10/mapreduce-reduced-ported-to-r/
.. [#f3] https://r-forge.r-project.org/R/?group_id=409
.. [#f4] http://www.stat.purdue.edu/~sguha/rhipe/


Examples
--------

Simple mapper and reducer
^^^^^^^^^^^^^^^^^^^^^^^^^

Simple example from "High Performance Computing in Statistics" course webpage maintained by `Luke Tierney at University of Iowa <http://www.stat.uiowa.edu/~luke/classes/295-hpc/>`_ . For more information
`see this AWS thread <https://forums.aws.amazon.com/thread.jspa?messageID=129163>`_ .

**mapper.py**

.. code-block:: r

	#! /usr/bin/env Rscript

	trimWhiteSpace <- function(line) gsub("(^ +)|( +$)", "", line)
	splitIntoWords <- function(line) unlist(strsplit(line, "[[:space:]]+"))
	    
	## **** could wo with a single readLines or in blocks
	con <- file("stdin", open = "r")
	while (length(line <- readLines(con, n = 1, warn = FALSE)) > 0) {
	    line <- trimWhiteSpace(line)
	    words <- splitIntoWords(line)
	    ## **** can be done as cat(paste(words, "\t1\n", sep=""), sep="")
	    for (w in words)
		cat(w, "\t1\n", sep="")
	}
	close(con)

**reducer.py**

.. code-block:: r

	#! /usr/bin/env Rscript

	trimWhiteSpace <- function(line) gsub("(^ +)|( +$)", "", line)

	splitLine <- function(line) {
	    val <- unlist(strsplit(line, "\t"))
	    list(word = val[1], count = as.integer(val[2]))
	}
	    
	env <- new.env(hash = TRUE)

	con <- file("stdin", open = "r")
	while (length(line <- readLines(con, n = 1, warn = FALSE)) > 0) {
	    line <- trimWhiteSpace(line)
	    split <- splitLine(line)
	    word <- split$word
	    count <- split$count
	    if (exists(word, envir = env, inherits = FALSE)) {
		oldcount <- get(word, envir = env)
		assign(word, oldcount + count, envir = env)
	    }
	    else assign(word, count, envir = env)
	}
	close(con)

	for (w in ls(env, all = TRUE))
	    cat(w, "\t", get(w, envir = env), "\n", sep = "")
