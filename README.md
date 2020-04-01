# Environmental Informatics

## Assignment 10 - Descriptive Statistics and Environmental Metrics

### Lab Objectives

On completion of this lab, students will be able to:

1. Calculate descriptive statistics for a dataset;
3. Calculate streamflow metrics further describing the distribution of daily streamflow and taht are correlated with aquatic ecosystem health; and
3. Generate summary tables that put the streamflow data into context using statistics and metrics.

### Reading Assignment

For descriptive statistics, you can start with any basic statistics textbook, as they will all discuss the concepts of measuring the central tendency and variability of a dataset.  For a brief review of the concepts in the context of data science (or informatics), check out:

- [Introduction to descriptive statistics](https://towardsdatascience.com/intro-to-descriptive-statistics-252e9c464ac9)

For environmental metrics, please read these two papers by Derek Booth and two of his students (posted to Blackbaord under Reading Materials -> Analysis Metrics).  Both seek to identify environmental metrics with predictive ability for water quality.  The first uses metrics to quantify the most ecologically significant changes in daily streamflow characteristics, while the second quantifies observed differences in land use in the upstream area near sampling sites.

- Konrad, C.P. and Booth, D.B. (2005) Hydrologic Changes in Urban Streams and Their Ecological Significance. American Fisheries Society Symposium, 47, 157-177.

- McBride, M. and Booth, D.B. (2005), URBAN IMPACTS ON PHYSICAL STREAM CONDITION: EFFECTS OF SPATIAL SCALE, CONNECTIVITY, AND LONGITUDINAL TRENDS1. JAWRA Journal of the American Water Resources Association, 41: 565-580. [doi:10.1111/j.1752-1688.2005.tb03755.x](doi:10.1111/j.1752-1688.2005.tb03755.x)

### The Lab Assignment

This week’s assignment is to calculate basic descriptive statistics and environmental metrics for two rivers with similar climate and drainage areas.  Do this by reading the two files into your Python code, checking for gross errors, clipping the two datasets to a consistent time period, and calculating the prescribed statistics and metrics.  

1. Use the files **TippecanoeRiver_Discharge_03331500_19431001-20200315.txt** and **WildcatCreek_Discharge_03335000_19540601-20200315.txt** provided with this repository.

   - These files contain daily discharge in cubic feet per second (cfs) for a single USGS gaging station.
   - Data file is white space delimited.
   - Column order and units are provided in the file header.
     
2. Modify the Python script template called program-10_template.py to complete this assignment.  The template contains code defining function names and input/output parameters, as well as comment text describing what each function should accept as parameters, return as variables, and functionally what each function should do.  **DO NOT** change the name or order of the parameters being sent to or from each function.  The template defines functions that the autograder program is going to import and evaluate.  Changing the program name or the function definitions, will cause the autograder to fail even if your code "works" for you.  

2. Copy the Python script template to a new script called **program-10.py** in the same folder, and edit this script so that it does the following:

   - Imports both streamflow file as DataFrames, using date as the index.  
     - Use two datafames, or a list of dataframes so that the dataframe containing streamflow from each river can be processed by each of the following functions.
     - Make sure that this function removes invalid streamflow data values.  The USGS file typically skips days with no measurement, but there are times when non-number values are used to fill for the discharge measurement when a final decision on its availability or quality has not been made.
     - Modify the provided function `ReadData()` to remove negative streamflow values as a gross error check.
     - Report only the total number of days missing observations at the end of the function, you do not need to count those failing the gross error check separately.
   - Complete the function `ClipData` to clip the data to the date range: October 1, 1969 through September 30, 2019.  This will provide you with 50 water years of streamflow data for your analysis.  The USGS defines a waer yaer as starting on October 1 of any year, for example the water year 2010 started on October 1, 2010 and ran throgh September 30, 2011.
   - Complete the function `GetAnnualStatistics` to build a new dataframe to contain annual (water year) values for the following metrics:
     
     | Full Name | Table Name | Description |
     |-----|-----|-----|
     | Annual Mean Flow | `Mean Flow` | Average annual streamflow for a given year. Can apply standard Pandas function. |
     | Annual Peak Flow | `Peak Flow` | Maximum streamflow value in a given year. Can apply standard Pandas function. |
     | Annual Median Flow | `Median Flow` |  Median streamflow value in a given year. Can apply standard Pandas function. |
     | Coefficient of Variation | `Coeff Var` | Coefficient of variation of streamflow in a given year. Calculated as the standard deviation divided by the mean annual streamflow multiplied by 100. |
     | Skewness | `Skew` | The skewness of the dataset.  Can make use of the SciPy Stats skew function. |
     | T-Qmean | `Tqmean` | The fraction of time (days) that streamflow exceeds mean annual streamflow (Qmean).  Complete the function `CalcTqmean` to accept a Series of daily streamflow values, calcualte the mean flow, and return the number of days on which daily streamflow is greater than the mean flow. |
     | Richards-Baker Flashiness Index | `R-B Index` | This is a measure of how much streamflow can change in a day ('flashiness').  Complete the function `CalcRBindex` to accept a Series of daily streamflow values, and return the R-B Index value.  The R-B Index is calculated by dividing the sum of the absolute values of day-to-day streamflow change by total discharge volumes for each year. |
     | 7-day Low Flow | `7Q` | The 7-day low flow is a common measurement of low flow in stream dsicharge, as metircs like minimum daily flow can fail as no flow or flow taht is too low to measure is not unexpected in some cases.  Complete the function `Calc7Q` to accecpt a Series of Daily streamflow values, and return the 7-day low flow value. The index is calculated by computing a 7-day moving average for the annual dataset, and picking the lowest average flow in any 7-day period. |
     | Flow Exceeding 3 Times Median Flow | `3xMedian` | This is a measure of the frequency of high flow (but not necessarily the highest flow) events.  Compelte the function `CalcExceed3TimesMedian` to accept a Series of daily streamflow values, and return the number of days that streamflow exceeds 3 times the median flow of the same period. |
     
     - Look into using the Pandas [`resample` method](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#resampling) to aggregate your daily time series into annual values.  You will want to review *Anchored Offsets* for appropriate ways to sample data and maintain the Water Year using October 1 as the anchor for resultant dates. Pandas functions such as `mean` can be applied directly during the resample process, but to apply your custom built functions look into the Pandas `apply` method. 
     
   - Complete the function `GetMonthlyStatistics` to build a new dataframe to contain monthly values for the following descriptive statistics and metrics:
   
     | Full Name | Table Name | Description |
     |-----|-----|-----|
     | Annual Mean Flow | `Mean Flow` | Average annual streamflow for a given year. Can apply standard Pandas function. |
     | Coefficient of Variation | `Coeff Var` | Coefficient of variation of streamflow in a given year. Calculated as the standard deviation divided by the mean annual streamflow multiplied by 100. |
     | T-Qmean | `Tqmean` | The fraction of time (days) that streamflow exceeds mean annual streamflow (Qmean).  Complete the function `CalcTqmean` to accept a Series of daily streamflow values, calcualte the mean flow, and return the number of days on which daily streamflow is greater than the mean flow. |
     | Richards-Baker Flashiness Index | `R-B Index` | This is a measure of how much streamflow can change in a day ('flashiness').  Complete the function `CalcRBindex` to accept a Series of daily streamflow values, and return the R-B Index value.  The R-B Index is calculated by dividing the sum of the absolute values of day-to-day streamflow change by total discharge volumes for each year. |
    
     -  This function should be very similar to the annual version, but reporting for months.  Theere should be no reason to rewrite any of the metric calulation functions, if you wrote them to work with *any* length data series provided.
     
   - Complete the fucntion `GetAnnualAverages` and `GetMonthlyAverages` to compute annual average values for all metrics.  
     - Annual average function should return a Series with a single average value for each statistic of metric.
     - Monthly average function should return a DataFrame with 12 monthly values for each metric.
     
3. Output the annual and monthly metrics tables to CSV files in the current directory.

4. Output the annual and monthyl averages to CSV files in the current directory.

5. Be sure that the script has a complete header comment block, appropriate in-line comments, and runs without intervention relative to where the datafile is stored in the repository.

#### What to turn in...

The following should be included in your GitHub repository:

1. A working program called **program-10.py**, which conforms to the template provided with the original repository.

2. The original data files, **TippecanoeRiver_Discharge_03331500_19431001-20200315.txt** and **WildcatCreek_Discharge_03335000_19540601-20200315.txt**, provided with the repository.

3. The four output CSV files from the program.

4. Put your input file, output files, and processing script in the assignment repository and push to GitHub. 

5. The instructor will follow-up with an invitation to submit the assignment through GradeScope.  Follow the provided instructions to submit the assignment using GitHub.  The AutoGrader will return a report on whether the submitted code met the performance checks.  If errors are found, fix the code, and resubmit.

#### Grading Rubric (50 pts Total)

| Question | Description | Score |
| -------- | ----------- | ----- |
| 1. | Write a Python script to complete the following analysis | (33.0 pts) |
| 1.1. | Import the entire file in as a DataFrame, using date as the index | 3.0 pts |
| 1.2. | Remove No Data values (set to -999) | 2.5 pts |
| 1.3. | Check 1: Check for gross errors: 0 ≤ P ≤ 25; -25≤ T ≤ 35, 0 ≤ WS ≤ 10 | 5.0 pts |
| 1.4. | Check 2: Swap Tmax and Tmin when Tmax is less than Tmin | 5.0 pts |
| 1.5. | Check 3: Check for temperature range greater than 25°C | 5.0 pts |
| 1.6. | Where a check is failed, replace value with NaN and record the number of data points replaced for each check. | 2.5 pts |
| 1.7. | Plot each dataset before and after correction has been made.  Use a single set of axis for each variable, and provide a legend that indiactes which is the original and which is after quality checking.  | 5.0 pts |
| 1.8. | Output data that has passed the quality check into a new file with the same format as the input data file. | 5.0 pts |
| 1.9. | Output information on failed checks to a separate Tab delimited file that can be imported into your Metadata file. | 5.0 pts |
| 2. | Working program | 5.0 pts |
| 3. | Program should have clear and concise header and in-line comments | 2.5 pts |
| 4. | Metadata file (PDF) that contains: | (7.5 pts) |
| 4.1. | Description of the data quality checks performed and how they influenced the contents of the file. | 2.5 pts |
| 4.2. | Table with the number of corrections made for all three checks. | 2.5 pts |
| 4.3. | Plots for each variable before and after quality checking. | 2.5 pts |
| 5. | Tried GradeScope submission. | 2.0 pts |
