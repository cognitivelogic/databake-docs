Columns
=======

A key ingredient of DataBake is the columns tab, which allows users to define the columns of their data schema and how they are generated as well as any post-generation operations to apply. Columns can be selected from a pool of `pre-defined`_ variants or defined explicitly as `custom`_ columns. Currently there is a limit of 20 columns that can be added to a table.

Pre-defined
-----------

A number of pre-defined column types are available that can be easily added to your schema. These column types have been selected based on the types of customer data companies will typically collect. These columns can also be tweaked through the insight tab - in the same way as `custom`_ columns and can be renamed during creation.

Custom
------

Alternatively, column types can be defined manually in custom mode. From the custom tab, in addition to specifying a column name, you can choose your `providers`_ and `wrappers`_ to define the ways in which the data will be generated. Values for the column can then be tweaked with :doc:`insights`.

Providers
^^^^^^^^^

Providers are functions which generate random values for the columns. They allow preformatted standard strings or numerical values to be added to a dataset with minimal configuration.

Basic
^^^^^

.. table:: Basic providers

    ==============================   ========================================================================================
    Function                         Effect
    ==============================   ========================================================================================
    Custom                           Returns a single value, very useful when combined with Insights.
    ISO Date                         Generates a timestamp between the 1st of January 1970 and the time of generation.
    String                           Returns a string specified by the formatting::

                                        ? will be replaced a random letter
                                        # will be replaced a random digit
                                        E.g. ####-???-ABCD
                                        => '7432-YGL-ABCD'
    Location                         Generates a random latitude longitude pair.
    ==============================   ========================================================================================

Profile
^^^^^^^

.. table:: Profile providers 

    ==============================   ========================================================================================
    Provider                         Effect
    ==============================   ========================================================================================
    Address                          Generates a random address.
    Job                              Generates a random job title.
    Last Name                        Generates a random last name.
    Email                            Generates a random email address.
    Name                             Genetates a random full name.
    Phone Number                     Generates a random phone number.
    Social Security Number           Generates a random social security number (or national equivalent).
    ==============================   ========================================================================================

For all of these providers an optional locale can be set which will generate values specific to that location.

Distributions
^^^^^^^^^^^^^

These providers will sample a distribution to generate random values. Parameters can be tweaked through Insights, but only a single sample can be returned per entry.

.. table:: Distribution providers

    ==============================   ========================================================================================
    Distribution                     Effect
    ==============================   ========================================================================================
    Uniform                          Generates values from a uniform distribution (see :func:`numpy.random.uniform`).
    Normal                           Generates values from a normal distribution (see :func:`numpy.random.normal`).
    Log Normal                       Generates values from a log normal distribution (see :func:`numpy.random.lognormal`).
    Beta                             Generates values from a beta distribution (see :func:`numpy.random.beta`).
    Gamma                            Generates values from a gamma distribution (see :func:`numpy.random.gamma`).
    ==============================   ========================================================================================


Choice Distributions
^^^^^^^^^^^^^^^^^^^^

Choice distributions are some of the most convoluted but powerful providers which allow relationships to applied from continuous values to discrete ones. 

.. table:: Choice distribution providers

    ==============================   ========================================================================================
    Distribution                     Effect
    ==============================   ========================================================================================
    Choice Distribution              Bisect a list at a point from a uniform distribution.
    Beta Choice Distribution         Bisect a list at a point from a beta distribution.
    Triangular Choice Distribution   Bisect a list at a point from a triangular distribution.
    ==============================   ========================================================================================

Wrappers
--------
Wrappers allow for a series of operations to be applied to each value generated for a column. These will be applied in the sequence in which they are added.

At this time the following operations are available:


.. table:: Wrappers

    ==============================   ========================================================================================
    Wrapper                          Effect
    ==============================   ========================================================================================
    add                              Offset the value by a float or int.
    multiply                         Multiply the value by a float or int.
    max                              Filter out results greater than a maximum.
    min                              Filter out results smaller than a minimum.
    round                            Reduce a float value to a number of digits after the decimal point.
    ==============================   ========================================================================================


If the requested operation cannot be applied to the value a None type will be returned instead.
