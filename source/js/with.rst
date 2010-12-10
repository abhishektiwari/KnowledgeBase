.. _jswith:

JavaScript with statement
=========================
The with statement is used to temporarily modify the scope chain. In practice, you can use the with statement to save yourself a lot of typing. In client-side JavaScript, for example, it
is common to work with deeply nested object hierarchies. 

*Example 1*


.. code-block:: javascript

	markupbuilder.div(
	  markupbuilder.p('Hi! I am a paragraph!',
	    markupbuilder.span('I am a span inside a paragraph')
	  )
	)

You could instead write:

.. code-block:: javascript

	with(markupbuilder){
	  div(
	    p('Hi! I am a paragraph!',
	      span('I am a span inside a paragraph')
	    )
	  )
	}


*Example 2*


You may have to type expressions like this one to access elements of an HTML form:

.. code-block:: javascript

	frames[1].document.forms[0].address_field.value

If you need to access this form a number of times, you can use the with statement to add the form to the scope chain:

.. code-block:: javascript

	with(frames[1].document.forms[0]) {
	// Access form elements directly here. For example:
	name.value = "";
	address.value = "";
	email.value = "";
	}

This reduces the amount of typing you have to do and you no longer need to prefix each form property name with frames[1].document. forms[0]. That object is temporarily part of the scope chain and is automatically searched when JavaScript needs to resolve an identifier like address_field.

Issues
------
Despite its occasional convenience, the use of the with statement is frowned upon. JavaScript code that uses with is difficult to optimize, and may therefore run more slowly than the equivalent code written without the with. Furthermore, function definitions and variable initializations within the body of a with statement can have surprising and counterintuitive behavior. For these reasons, therefore, it is recommended that you avoid the with statement.

Note that there are other, perfectly legitimate ways to save yourself typing. The with example 2 above could be rewritten as follows:

.. code-block:: javascript

	var form = frames[1].document.forms[0];
	form.name.value = "";
	form.address.value = "";
	form.email.value = "";
