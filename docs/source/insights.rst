Insights
========

For some :doc:`columns` it is possible to modify the method by which values are generated through the *Insights* tab. The most basic way of doing so is to tweak the literal parameters of the generation function. For example, if we had a column where values were generated as random points on a normal distribution through the normal distribution provider, we would be able to modify the mean and the standard deviation of the distribution.

If possible, the expression for the function parameter will be processed with :func:`ast.literal_eval` and passed to the function each time a new value is generated, allowing for some basic operators to be used while still preserving performance. This allows python syntax literals to be used without much effect on performance, such as::

    5
    3.14
    7.4E-9
    [1, 2]
    'abc'
    3 + 1

However, if the resulting expression cannot be used as an argument for the function an error will be raised and a preview will not be generated. When modifying these values a small preview graph will be generated that will give a helpful plot of the shape of the expected distribution.

For additional reference about the types of functions provided and their arguments, see :mod:`faker.providers` and :mod:`numpy.random`.

Choices
-------

A special case of insight is when using the choices providers. By default each item will have an equal probability (before any bias is applied from a distribution), but this can be altered from the insights tab. 

When creating an insight for a column that uses a choice provider, in addition to any other provider variables, you will also be able to modify the ratios at which the each of the items is likely to be generated as a value.

Relationships
-------------

The most powerful aspect of *Insights*, however, is the ability to add relationships between columns in order to build dependent variables into your datasets. Using this feature will mean that the arguments passed to the generation function will be updated for each value generated which will take longer to process than just using literal values. Supposing that you have already defined three columns, *age*, *average_product_price*, and *favourite_product*, a simple relationship between the age of the customers in our dataset and the price of the products that they are buying.

.. graph:: unconnected_columns

   "age"
   "average_product_price"
   "favourite_product"

This is performed by creating an Insight for *average_product_price* and setting one of the arguments in the provider to be derrived from the *age* column. This will mean that each time a value for *average_product_price* is generated for the dataset the value in the age column will be used as a factor for generation. For example, if our *average_product_price* used a `normal distribution <https://en.wikipedia.org/wiki/Normal_distribution>`_ to generate values, we could make the standard deviation argument in the generation function to a multiple of age, meaning that there would be a greater range of average purchase as people grew older. Effectively, this Insight could be visualised as a connection between the two variables in a directed graph.

 .. digraph:: connected_columns
    
    "age" -> "average_product_price"
    "favourite_product"

Extending this idea further, more relationships can be added between *favourite_product* and the other two columns. Not only can this be done through having a source for each variable, but the two variables can even be combined with one another. These relationships will be resolved by the platform before generation and used to generate each column in order, but it means there is an important condition that the relationships between columns must form a `directed acyclic graph <https://en.wikipedia.org/wiki/Directed_acyclic_graph>`_ such that no variable is dependent upon itself. 

 .. digraph:: connected_columns
    
    "age" -> "average_product_price" -> "favourite_product"
    "age" -> "favourite_product"

Handily, DataBake will visualise a simplified version of these relationships in a graph on the left hand side of the page under the heading of **Column Relationships**. Here you will be able to see how each column is connected to one another as well as their relationships


Additional features
-------------------