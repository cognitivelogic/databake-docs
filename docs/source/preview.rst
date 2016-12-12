Preview
=======

The preview tab lets you see an example of a small dataset of 100 rows generated from your project settings which allows you to get an idea of a sample of what your dataset might look like without committing to generating it in full. This is very useful when checking for data nullified by wrappers and catching errors.

Charts
------

A few charts are available for most columns that will display the preview data on histograms or fitted curve plots, these charts are from a larger set of 1000 rows and normalised in order to reduce the effect of noise on the shape of the distribution. These charts will give you a good idea as to what the shape of the distributions in your final dataset will be so that it is easy to get quick feedback on your distributions so that it is adjustable. In addition to the histogram, a gaussian `kernel density estimator <https://en.wikipedia.org/wiki/Kernel_density_estimation>`_ (KDE) will be plotted on the graph that will give the distribution a smoother shape for visualisation.

Data
----

Alternatively, you can see a sample of the kind of data created from the data tab. This will show you a table of the 100 preview rows so that you can see the underlying data. 

Scatter plots
-------------

When you have multiple distributions in your dataset, scatter plots of each column will become available, allowing you to easily visualise the correlations between columns in the generated data. To allow flexibility in this view, you can deselect columns you are not interested in seeing as well as colour coding the points by categorical data. 
