.. _neo4jinstall:

Installing Neo4j
================

Without Maven
-------------

If you don't use Maven: Download the  Apoc version or neo4j-apoc-* release which containts Neo4j together with the most used add-on libraries. Add the Neo4j kernel and JTA jars to your classpath. Apoc is A Package Of Components, i.e. a handful of useful Neo4j components bundled together in one convenient package. Apoc currently includes following components:
	* neo4j-kernel -- the Neo4j kernel
	* neo4j-index -- an indexing component that lets you look up nodes by property value
	* neo4j-shell -- a command line browser that allows you to connect to a running Neo4j instance and browse the graph using familiar Unix commands like ls, cd and pwd
	* neo4j-remote-graphdb -- an implementation of the Neo4j API that delegates all operations to a remote Neo4j instance
	* neo4j-online-backup -- backup a running Neo4j instance (included since 1.1)
	* neo4j-graph-algo -- graph algorithms like shortest-path for Neo4j (included since 1.1)

.. code-block:: bash
	
	mkdir Neo4j
	cd Neo4j
	wget http://dist.neo4j.org/neo4j-apoc-1.1.tar.gz
	tar zxvf neo4j-apoc-1.1.tar.gz

Set the class path in your *~/.profile* or *~/.bashrc*

.. code-block:: bash

	#Neo4J
	export Neo4J=/your_home_directory/Neo4j/neo4j-apoc-1.1/
	export PATH=$PATH:$Neo4J/bin

Updates the changes

.. code-block:: bash 

	source ~/.bashrc

You can start the Neo4j Shell client by running *neo4j-shell* and it will ask that if you want to run a local shell intance (l) or to accept remote connection(r).

With Maven
----------

Coming soon

.. toctree::
   :maxdepth: 2

   
