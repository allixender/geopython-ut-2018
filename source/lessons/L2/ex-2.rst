Exercise 2
==========

This lesson we will focus on how to create geometries in Geopandas and how to re-project data and do some basic
geometric calculations.

- Don't forget to check out the `hints for this lesson's exercise <exercise-2-hints.html>`_ if you're having trouble.
- Scores on this exercise are out of **10 points**.

Sections
--------

 - `Problem 1: Create Polygon from lists of coordinates <#problem-1-create-polygon-from-lists-of-coordinates>`_
 - `Problem 2: Points to map <#problem-2-points-to-map>`_
 - `Problem 3: How long distance individuals have travelled? <#problem-3-movements-of-individual-user>`_

Problem 1: Create Polygon from lists of coordinates (3 points)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the first problem you should:

 - create a Polygon out of the the x and y coordinates that are provided in the ``create_polygon.py`` -script.
 - insert the polygon into a GeoDataFrame
 - save the Polygon into a Shapefile.
 - plot and save a figure out of the Polygon.

The `**create_polygon.py** <../../_static/exercises/Exercise-2/create_polygon.py>`_ starter script has all necessary steps listed and also some hints are provided.
There are all together 6 steps that you need to fill to accomplish the problem 1.
Each step that you need to fill is marked with capital P -letter (P1 to P6).

Problem 2: Points to map (3 points)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The problem 2 this lesson continues the process that we started last lesson, i.e. creating geometric point -objects and putting them into a map.
Here our aim is to plot a set of x and y coordinates that we should read from the `**some_posts.csv** <../../_static/exercises/Exercise-2/data/some_posts.csv>`_ comma separated file that contains following kind of data:

.. code::

    lat,lon,timestamp,userid
    -24.980792492,31.484633302,2015-07-07 03:02,66487960
    -25.499224667,31.508905612,2015-07-07 03:18,65281761
    -24.342578456,30.930866066,2015-03-07 03:38,90916112
    -24.85461393,31.519718439,2015-10-07 05:04,37959089


The data has 81379 rows and consists of locations and times of social media posts inside Kruger national park in South Africa:

+------------------+---------------------------------------------------------+
| Column           | Description                                             |
+==================+=========================================================+
| lat              | y-coordinate of the post                                |
+------------------+---------------------------------------------------------+
| lon              | x-coordinate of the post                                |
+------------------+---------------------------------------------------------+
| timestamp        | Time when the post was uploaded                         |
+------------------+---------------------------------------------------------+
| userid           | userid                                                  |
+------------------+---------------------------------------------------------+

.. note::

    although the data is based on real social media data, it is heavily anonymized. Userids and timestamps have been randomized, i.e. they do not not match with real ones,
    also spatial accuracy of the data have been lowered.


- `Download the data **some_posts.csv** <../../_static/exercises/Exercise-2/data/some_posts.csv>`_ (Click on the link ==> CNTRL + S)
- Read the data into memory using Pandas
- Create an empty column called ``geometry`` where you will store shapely Point objects
- Iterate over the rows of the DataFrame and insert Point objects into the column geometry (you need to use .loc indexer to update the row, `see materials <geopandas-basics.html#creating-geometries-into-a-geodataframe>`_
- Convert that DataFrame into a GeoDataFrame, `see hints <exercise-2-hints.html>`_
- Update the CRS for coordinate system as WGS84 (i.e. epsg code: 4326)
- Save the data into a Shapefile called ``Kruger_posts.shp``
- Create a simple map of those points using a GIS software or using ``.plot()`` -funtion in Python. Save it as a png file.


Problem 3: How long distance individuals have travelled? (4 points)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this problem the aim is to calculate the distance in meters that the individuals have travelled according the social
media posts (Euclidian distances between points).

Write your codes into the same file as in previous Problem (2).

In your code you should:

 - Reproject the data from WGS84 into ``EPSG:32735`` -projection which stands for UTM Zone 35S (UTM zone for South Africa) to transform the data into a metric-based system.
 - Group the data by userid
 - Create an empty GeoDataFrame called ``movements``
 - Set the CRS of the ``movements`` GeoDataFrame to ``EPSG:32735`` (epsg code: 32735)

 - For each user:
    - `sort <http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.sort_values.html>`_ the rows by timestamp
    - create LineString objects based on the points
    - `add <http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.append.html>`_ the geometry and the userid into the GeoDataFrame you created in the last step
 - Calculate the lenghts of the lines into a new column called ``distance`` in ``movements`` GeoDataFrame.
 - Save the movements of into a Shapefile called ``Some_movements.shp``


Questions
---------

Write your answers below the solved problems in your code file.
You should also print the answers to the questions in your code.

 - What was the shortest distance travelled in meters?
 - What was the mean distance travelled in meters?
 - What was the maximum distance travelled in meters?

