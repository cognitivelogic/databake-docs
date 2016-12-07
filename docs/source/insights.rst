Insights
========

DataBake can generate insights in your dataset by through a range of methods.

The simplest method is defining the literal arguments - which can give you a constant value for a variable in a generation function. For example, a variable with normal distribution can be changed to show insights by changing the mean and standard deviation of the :doc:`columns`.

The expressions which define the functions's arguments are processed using :func:`ast.literal_eval`. These are then passed to the function where the new values are generated. This allows for some basic operators to be utilised - while still maintaining a good level of performance. Some examples of the types of literals that can be used in this way are::

    5
    3.14
    7.4E-9
    [1, 2]
    'abc'
    3 + 1

For more details see the python documentation of :func:`ast.literal_eval`.

When modifying the variables, a small preview graph will be generated to give a helpful plot of the shape of the expected distribution. However, if the resulting expression cannot be used as an argument for the function, the server will return an error and a preview will not be displayed.

For additional information about the types of functions provided and their arguments, see :doc:`columns`.

Choices
-------

Another way of generating insights is by using the choice providers.

Before any bias is applied, each item will have an equal chance by default. When using a choice provider to determine a columns’ insight, you will be able to change the ratios at which the items are likely to be generated as a value. This can be in addition to any other providers.

Relationships
-------------

The most powerful aspect of *Insights* is the ability to add relationships between columns to build dependent variables into your datasets. Using this feature, the arguments passed to the generation function will be updated for each value - which will take longer to process than just using literal arguments.

Supposing that you have already defined three columns, *age*, *average_product_price*, and *favourite_product*, you can now define a simple relationship between the age of the customers in our dataset and the price of the products they are buying.

.. graph:: unconnected_columns

   "age"
   "average_product_price"
   "favourite_product"

This is performed by creating an insight for *average_product_price* and setting one of the arguments in the provider to be derived from the *age* column. This will mean that each time a value for *average_product_price* is generated for the dataset, the value in the age column will be used as a contributing factor.

For example, if *average_product_price* uses a normal distribution to generate values, a relationship could be added to make average product price a multiple of age - meaning that there would be a larger range of average purchase prices as people grow older.

This insight could be visualised as a connection between the two variables in a directed graph.

 .. digraph:: connected_columns

    "age" -> "average_product_price"
    "favourite_product"

Extending this idea further, more relationships can be added between *favourite_product* and the other two columns. Not only can this be done through having a source for each variable, but the two variables can even be combined with one another.

These relationships are defined before generation and used to order each generated column, but it means there is an important condition that the relationships between columns must form a `directed acyclic graph <https://en.wikipedia.org/wiki/Directed_acyclic_graph>`_ - such that no variable is dependent upon itself.

 .. digraph:: connected_columns

    "age" -> "average_product_price" -> "favourite_product"
    "age" -> "favourite_product"

DataBake will display a simplified version of these relationships in a graph on the left hand side of the page under the heading of **Column Relationships**. Here you will be able to see how each column connects to one another, including the expression that dictates their relationship.


Additional features
-------------------

In order to provide flexibility in dataset creation a number of extra functions are available for use in Insights.

Builtins
^^^^^^^^

====================  ===========================================================================================
Function              Effect
====================  ===========================================================================================
:func:`abs`           Returns the absolute value of a numerical object.
:func:`all`           Returns true if all conditions in an iterable are met.
:func:`any`           Returns true if any conditions in an iterable are met.
:func:`chr`           Returns the string character of an integer.
:func:`dir`           Returns the list of names in the current scope.
:func:`hash`          Returns the hash value of the object.
:func:`len`           Returns the number of items of an object.
:func:`max`           Returns the largest value in an object.
:func:`min`           Returns the smallest value in an object.
:func:`ord`           Returns integer representation of a unicode character.
:func:`pow`           Returns the first argument to the power of the second.
:func:`round`         Returns the first value rounded to digits specified by the second.
:func:`sorted`        Returns a sorted version of an object.
:func:`sum`           Returns the sum of all objects.
====================  ===========================================================================================

Type Conversion
^^^^^^^^^^^^^^^

====================  ===========================================================================================
Function              Effect
====================  ===========================================================================================
:func:`bin`           Converts an integer number to a binary string.
:func:`bool`          Converts a value to boolean.
:func:`complex`       Converts a value to a complex number.
:func:`float`         Converts a value to a floating point number.
:func:`hex`           Converts a value to its hex representation.
:func:`int`           Converts a value to an integer.
:func:`oct`           Converts a value to its oct representation.
:func:`str`           Converts a value to a string.
====================  ===========================================================================================


Statistical
^^^^^^^^^^^

============================================  ===========================================================================================
Function                                      Effect
============================================  ===========================================================================================
:func:`normal <numpy.random.normal>`          Draws random samples from a normal distribution.
:func:`triangular <numpy.random.triangular>`  Draws random samples from a triangular distribution.
:func:`uniform <numpy.random.uniform>`        Draws random samples from a uniform distribution.
:func:`poisson <numpy.random.poisson>`        Draws random samples from a poisson distribution.
:func:`beta <numpy.random.beta>`              Draws random samples from a beta distribution.
============================================  ===========================================================================================

