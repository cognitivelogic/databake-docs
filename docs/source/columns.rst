Columns
=======

A key ingredient of DataBake is the columns tab, which allows users to define the columns of their data schema and how they are generated as well as any post-generation operations to apply. Columns can be selected from a pool of `pre-defined`_ variants or defined explicitly as `custom`_ columns. Currently there is a limit of 20 columns that can be added to a table.

Pre-defined
-----------

A number of pre-defined column types are available that can be easily added to your schema. These column types have been selected based on the types of customer data companies will typically collect. These columns can also be tweaked through the insight tab - in the same way as `custom`_ columns and can be renamed during creation.

Custom
------

Alternatively, column types can be defined manually. Users can add `providers`_ and `wrappers`_ to define the ways in which the data will be generated.

Providers
^^^^^^^^^
(Need a big reference manual)

Providers are functions which generate random values.

Locales
^^^^^^^

Formatters
^^^^^^^^^^

Distributions
^^^^^^^^^^^^^



Choice Distributions
^^^^^^^^^^^^^^^^^^^^

Wrappers
--------
Wrappers allow for a series of operations to be applied to each value generated for a column. These will be applied in the sequence in which they are added.

At this time the following operations are available:

===========   ======================================================================
Wrapper       Effect
===========   ======================================================================
add           offset the value by a float or int.
multiply      multiply the value by a float or int.
max           filter out results greater than a maximum.
min           filter out results smaller than a minimum.
round         reduce a float value to a number of digits after the decimal point.
===========   ======================================================================


If the requested operation cannot be applied to the value a None type will be returned instead.
