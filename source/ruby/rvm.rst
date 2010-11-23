.. _rvm:

Ruby version manager
====================

1. To install/update RVM from the github repository (recommended):

.. code-block:: bash

	bash < <( curl http://rvm.beginrescueend.com/releases/rvm-install-head )

2. After installing RVM, add following line to your profile at the very end, after all path loads etc:

.. code-block:: bash

	[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"

Drop above line into your ~/.profile or ~/.bashrc file. Use . ~/.profile or source ~/.bashrc in terminal to update the settings.
3. Install the Ruby version

.. code-block:: bash

	rvm install 1.8.7
	rvm install 1.9.1
	rvm install jruby

4. To switch between different versions of Ruby

.. code-block:: bash

	rvm use 1.8.7
	rvm use 1.9.1
	rvm use jruby

5. Setting the default Ruby, simply use the --default flag:

.. code-block:: bash

	rvm use 1.8.7 --default 
	ruby -v

6. Listing the rubies,

You can view the commands available by typing

.. code-block:: bash

	rvm list

To list all installed rubies

.. code-block:: bash

	rvm list rubies

To list the default ruby

.. code-block:: bash

	rvm list default

To list the default ruby string only

.. code-block:: bash

	rvm list default string

To list all installed rubies, in their ruby string representation only

.. code-block:: bash

	rvm list strings

To list all *known* RVM installable Rubies

.. code-block:: bash

	rvm list known

7. RVM has “gemsets” which allow you to organize different sets of gems. If you install gems into the global gemset, then it will be available to you no matter which gemset you are using. To create the global gemset.

.. code-block:: bash

	rvm gemset create globalt
	rvm gemset use globalt

Install gems here that will be used in most of projects like bundler and passenger.

.. code-block:: bash

	gem install bundler
	gem install passenger

Note that rvm puts these gemsets in your user ~/.rvm directory. You can create and use your project specific gemset.

.. code-block:: bash

	rvm gemset create YOUR_GEMSET
	rvm gemset use YOUR_GEMSET

Alternatively we can switch to a gemset when we use a ruby by appending @YOUR_GEMSET to the end of the ruby selector string:

.. code-block:: bash

	rvm use 1.8.7@rails3
	rvm use 1.8.7@rails2

8. To list all named gem sets for current selected ruby interpreter

.. code-block:: bash

	rvm gemset list

9. To list the name of the currently selected gem set

.. code-block:: bash

	rvm gemset name

10. Benchmark your ruby script/project against multiple ruby versions,

.. code-block:: bash

	rvm 1.8.7,1.9.1,jruby code.rb

11. RVM allows you to run rake tasks, tests, specs across multiple ruby versions:

.. code-block:: bash

	rvm 1.8.6,1.9.1 rake test
	rvm 1.8.6,1.9.1 rake spec
	rvm 1.8.6,1.9.1 specs

12. To uninstall and remove rubies, remove clean everything the ruby, source files and optionally gemsets / archives while uninstall just removes the ruby - leaves everything else

.. code-block:: bash

	rvm remove jruby,1.8.7
	rvm uninstall jruby,1.8.7

13. To delete a gem set,

.. code-block:: bash

	rvm gemset delete YOUR_GEMSET
