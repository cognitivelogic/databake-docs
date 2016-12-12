Insights
========

DataBake can generate insights in your dataset by through a range of methods.

The simplest type of insight is defining the literal arguments - which can give you a constant value for a variable in a generation function. For example, a variable with based on a normal distribution can be changed to show insights by changing the mean and standard deviation of the :doc:`columns`.

The expressions which define the functions's arguments are processed using :func:`ast.literal_eval`. These are then passed to the function where the new values are generated. This allows for some basic operators to be utilised - while still allwowing your dataset to be generated as quickly as possible. Some examples of the types of literals that can be used in this way are::

    5
    3.14
    7.4E-9
    [1, 2]
    'abc'
    3 + 1

For more details see the python documentation of :func:`ast.literal_eval`.

When modifying the variables, a small preview graph will be generated to give a helpful in browser plot of the shape of the expected distribution. Once you add the insight this graph will then be derrived from a preview of the dataset. However, if the resulting expression cannot be used as an argument for the function, the server will return an error and a preview will not be displayed. 

For additional information about the types of functions provided and their arguments, see :doc:`columns`.

Choices
-------

Another way of generating insights is by using the choice providers.

Before any bias is applied, each item will have an equal chance by default. When using a choice provider to determine a columns’ insight, you will be able to change the ratios at which the items are likely to be generated as a value. This can be in addition to any other providers.

Relationships
-------------

The most powerful aspect of insights is the ability to add relationships between columns to build dependent variables into your datasets. Using this feature, the arguments passed to the generation function will be updated for each value. This has a substantial perfomance tradeoff compared to using constant expressions, but is necessary to create the most interesting datasets.

Supposing that you have already defined three columns, *age*, *average_product_price*, and *favourite_product*, you can now define a simple relationship between the age of the customers in our dataset and the price of the products they are buying.

.. graph:: unconnected_columns
    :align: center
    :caption: Unconnected columns.

    "age"
    "average_product_price"
    "favourite_product"

This relationship is added by creating an insight for *average_product_price* and setting one of the arguments in the provider to be derived from another column. The arguments for each provider will appear as forms inside the insights dialog window once a column is selected, where you can type in the column name you wish to derrive values from as a variable. For example, if we were to add an expression containing the column name 'age' as an argument, this will mean that each time a value for *average_product_price* is generated for the dataset, the value in the age column will be used to calculate each value for the column to which the insight has been added.

More specifically, if *average_product_price* uses a normal distribution to generate values, a relationship could be added to make average product price a multiple of age by entering 'age * 30' into the *Mean* box. Once the dataset is generated this would have the effect of simulating a larger range of average purchase prices as people grow older.

This insight could be visualised as a connection between the two variables in a directed graph.

.. digraph:: connected_columns
    :align: center
    :caption: A single relationship.

    "age" -> "average_product_price"
    "favourite_product"

Extending this idea further, more relationships can be added between *favourite_product* and the other two columns. Not only can this be done through having a source for each variable, but the two variables can even be combined with one another.

These relationships are resolved before generation and used to work out the order in which columns should be generated, but it means there is an important condition that the relationships between columns must form a `directed acyclic graph <https://en.wikipedia.org/wiki/Directed_acyclic_graph>`_ - such that no variable is dependent upon itself.

.. digraph:: connected_columns
    :align: center
    :caption: The complete relationships

    "age" -> "average_product_price" -> "favourite_product"
    "age" -> "favourite_product"

DataBake will display a simplified version of these relationships in a graph on the left hand side of the page under the heading of **Column Relationships**. Here you will be able to see how each column connects to one another, including the expression that dictates their relationship.

Editor
------

When editing column relationships in the insights dialog window, a few additional features are available. Arithmetic operators can be used in your expressions including modulo and indices, though it is important to note that there is an execution time limit for each cell so you will not be able to use generate datasets containing expressions like ``9**9**9**9**9**9**9`` as they will fail to preview. The ``==`` comparison operator is also available, primarily for string comparisons in column relatiponships.


Functions
---------

In order to provide flexibility in dataset creation a number of extra functions are available for use in insights.

Builtins
^^^^^^^^

Builtins are basic python functions for commonly used operations.

.. table:: Common builtin functions.

    ============================================  ===========================================================================================
    Function                                      Effect
    ============================================  ===========================================================================================
    :func:`abs`                                   Returns the absolute value of a numerical object.
    :func:`all`                                   Returns true if all conditions in an iterable are met.
    :func:`any`                                   Returns true if any conditions in an iterable are met.
    :func:`chr`                                   Returns the string character of an integer.
    :func:`dir`                                   Returns the list of names in the current scope.
    :func:`hash`                                  Returns the hash value of the object.
    :func:`len`                                   Returns the number of items of an object.
    :func:`max <numpy.amax>`                      Returns the largest value in an object.
    :func:`min <numpy.amin>`                      Returns the smallest value in an object.
    :func:`ord`                                   Returns integer representation of a unicode character.
    :func:`pow`                                   Returns the first argument to the power of the second.
    :func:`round`                                 Returns the first value rounded to digits specified by the second.
    :func:`sorted`                                Returns a sorted version of an object.
    :func:`sum`                                   Returns the sum of all objects.
    ============================================  ===========================================================================================

Type Conversion
^^^^^^^^^^^^^^^

Type conversions let you manipulate the kinds of data being passed into functions.

.. table:: Type functions.

    ============================================  ===========================================================================================
    Function                                      Effect
    ============================================  ===========================================================================================
    :func:`bin`                                   Converts an integer number to a binary string.
    :class:`bool`                                 Converts a value to boolean.
    :class:`complex`                              Converts a value to a complex number.
    :class:`float`                                Converts a value to a floating point number.
    :func:`hex`                                   Converts a value to its hex representation.
    :class:`int`                                  Converts a value to an integer.
    :func:`oct`                                   Converts a value to its oct representation.
    :class:`str`                                  Converts a value to a string.
    ============================================  ===========================================================================================


Statistical
^^^^^^^^^^^

Statisical functions let you draw values from distributions to be used as function arguments.

.. table:: Statistical functions.

    ============================================  ===========================================================================================
    Function                                      Effect
    ============================================  ===========================================================================================
    :func:`normal <numpy.random.normal>`          Draws random samples from a normal distribution.
    :func:`triangular <numpy.random.triangular>`  Draws random samples from a triangular distribution.
    :func:`uniform <numpy.random.uniform>`        Draws random samples from a uniform distribution.
    :func:`poisson <numpy.random.poisson>`        Draws random samples from a poisson distribution.
    :func:`beta <numpy.random.beta>`              Draws random samples from a beta distribution.
    ============================================  ===========================================================================================

