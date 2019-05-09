# NYC-Taxi-data---huge-dataset-visualization-using-Datashader-and-Bokeh
A fascinating side project visualizing millions of data points using Datashader

Below is the link to the reference python notebook. https://anaconda.org/jbednar/nyc_taxi/notebook 

* After downloading the notebook and reading about the exercise, I downloaded the file with all locations of all NYC taxi pickups and dropoffs from the month of March 2016 from the below link. It had over 12 million entries. http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml 
* Few columns from the original file were imported into a dataframe using pandas module. Initially, there were only latitude and longitude columns in it as shown below. 
* To map the co-ordinate information in a map, I had to convert latitude and longitude to web Mercator co-ordinates (used in google maps and other web applications). This turned out to be a time-consuming endeavor as there are many confusing co-ordinate systems. I had to create a user-defined function, after filtering out the null values in the data. Math turned out to be best package for this job as other packages such as pyproj and utm took hours to process 12 million entries. This piece of code was missing in the original notebook.

Scatterplots explored are -
* 1000-point scatterplot - It was interesting plotting with 1000 datapoints in the sample. As only 0.000083 %of the data from 12 million entries were represented, it lead to a phenomenon called undersampling shown in Figure (a). 
*10,000-point scatterplot – lead to a phenomenon called over-sampling and it was hard to view along with the map. 
* 100,000-point scatterplot – lead to saturation as the points became tiny and visible at popular locations.
* 10 million-point datashaded plots - with datashader, there comes features such as auto-ranging and we can plot large datasets without over-sampling, undersampling or saturation. Below are some of the plots of 10 million datapoints with varying range and parameters. They are generated in few seconds.

Interactive datashaded plots – Here is the unveiling of the full strength of datashader. It is interactive showing the different levels of the large dataset. It reveals local structures that are invisible through global view. Furthermore, it performs automatic operations and auto-ranging and optimates our output. We can further customize the plot by inserting Bokeh tile- STAMEN_TERRAIN (apparently by Stamen design) that inserts a map of the area under study / visualization. There were several errors during these steps due to an empty array passed from the aggregate parameter. Turned out to be incorrect x and y range in the plot definition. The final plot looks surreal and beautiful. The interactive features of bokeh and datashader can be used to view local structures. Even though the timing of the trip is color-coded (example: red at night, blue in the evening), there are busy hours that stand-out.
