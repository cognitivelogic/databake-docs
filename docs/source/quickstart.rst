Quickstart
==========

To get started, enter a project name under the 'Create a new project' heading and click 'Let's go'. This will enable you to track your projects and change the datasets later. Alternatively, you can load a template dataset.

.. image:: images/quickstart/createproject.png

Creating a new project will take you through to the main page - where you can define the variables and the insights in your personalised generated dataset. The overall project name is displayed on the top left-hand side. Below, you can re-name the table you are about to generate – this is especially relevant if you plan on generating multiple tables in the same project.

.. image:: images/quickstart/projectscreen.png

To the right of the project name, you will see four tabs titled 'Columns', 'Insights', 'Preview' and 'Export' respectively. These tabs will lead you through the process of generating a dataset using DataBake. Selecting the column tab, we will begin by defining the columns of our table.

You will also notice that a help icon on the top right of the column tab and in various other places throughout the site. This will lead to the documentation for that section if you need to gain more insight into the process. If the documentation is not able to help you can also send a support ticket through the tab on the right hand side of the page.

Firstly, define the column variables by clicking the 'Add' button underneath the 'Columns' tab. A dialog box will appear and, as you can see, there is a drop down menu containing a range of pre-defined columns arranged by group. There is also the option to generate your own customer columns.

.. image:: images/quickstart/createcolumn.png

For this example, the first pre-defined column we will be adding is **Name** - which creates a column filled with randomly generated full names. Click 'Submit' and a table with 'Name' in the column field will appear. You will notice that the option to pick a localisation setting for your generated names, this can be ignored for now but for more information see the providers sub-section of the :doc:`columns` documentation.

.. image:: images/quickstart/column.png

Next, click 'Add' again, scroll down the drop down menu to demographic data and select **Age**. Here you will notice that this column is based on a numerical distribution for which a histogram of values will be helpfully displayed under the heading of *Sample Data*, this  Click 'Submit' and the 'Age' column will appear in the same table as 'Name'. 

.. image:: images/quickstart/agecolumn.png

As an example, next 'Add' in a custom column. Type an example column name, such as 'Number'. Click on the 'Provider' drop down menu, and select 'Normal'. This will add a third column to the table.

.. image:: images/quickstart/threecolumns.png

Now the columns are defined, click on the 'Insights' tab to add the relationships between the variables. 

Click 'Add' and another dialog box will appear. Click on the 'Column' drop down menu and select 'Number'. In the 'Mean' box type ``1 * age``. As you type 'age', a blue box will appear below – click on this and the text will automatically update to ``1 * (Age)``. Click 'Submit' and a connection will be shown between 'Age' and 'Number' in the column relationships box on the left hand side. 

You can now click on 'Preview' to view your dataset and insights in a table and charts.
(screenshot of preview)

Finally, click the 'Export' tab to export your dataset and share DataBake on Facebook.
