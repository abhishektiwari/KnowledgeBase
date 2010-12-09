.. _jquery_tip1:

Document ready vs Window load
=============================

The document ready event executes already when the HTML-Document is loaded and the DOM is ready, even if all the graphics haven’t loaded yet. The window load event executes a bit later when the complete page is fully loaded, including all frames, objects and images.

Using jQuery
------------

Document ready
^^^^^^^^^^^^^^

.. code-block:: javascript

	$(document).ready(function() {
	 // Executes when HTML-Document is loaded and DOM is ready
	 alert("document is ready");
	});

Windows load
^^^^^^^^^^^^

.. code-block:: javascript

	$(window).load(function() {
	 // Executes when complete page is fully loaded, including all frames, objects and images
	 alert("window is loaded");
	});


Using Javascript
----------------

Windows load version
^^^^^^^^^^^^^^^^^^^^

In HTML section,

.. code-block:: html 

	<body onload='OnBodyLoad()'>

and in script section.

.. code-block:: javascript

	function OnBodyLoad()
	{
	  // Do something here
	}


Otherwise you can do it in a single step,

.. code-block:: javascript

	window.onload = function(){
	  // Do something here
	};

Document ready
--------------

All three of the following syntaxes are equivalent:

.. code-block:: javascript

	$(document).ready(handler) 
	$().ready(handler)             // this is not recommended
	$(handler)                     //handler is a function to execute after the DOM is ready. 

There is also $(document).bind("ready", handler). This behaves similarly to the ready method but with one exception: If the ready event has already fired and you try to .bind("ready") the bound handler will not be executed.

The .ready() method can only be called on a jQuery object matching the current document, so the selector can be omitted.

The .ready() method is typically used with an anonymous function:

.. code-block:: javascript

	$(document).ready(function() {
	  // Handler for .ready() called.
	});

If .ready() is called after the DOM has been initialized, the new handler passed in will be executed immediately.
