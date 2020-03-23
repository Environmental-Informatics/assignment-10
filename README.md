# Environmental Informatics

## Assignment 10 - Descriptive Statistics and Environmental Metrics

### Lab Objectives

On completion of this lab, students will be able to:

1. Calculate descriptive statistics for a dataset;
3. Calculate metrics describing ecosystem health; and
3. Generate summary figures that put data into context using statistics and metrics.

### Reading Assignment

For descriptive statistics, you can start with any basic statistics textbook, as they will all discuss the concepts of measuring the central tendency and variability of a dataset.  For a brief review of the concepts in the context of data science (or informatics), check out:

- [Introduction to descriptive statistics](https://towardsdatascience.com/intro-to-descriptive-statistics-252e9c464ac9)

For environmental metrics, please read these two papers by Derek Booth and two of his students.  Both seek to identify environmental metrics with predictive ability for water quality.  The first uses metrics to quantify the most ecologically significant changes in daily streamflow characteristics, while the second quantifies observed differences in land use in the upstream area near sampling sites.

- Konrad, C.P. and Booth, D.B. (2005) Hydrologic Changes in Urban Streams and Their Ecological Significance. American Fisheries Society Symposium, 47, 157-177.

- McBride, M. and Booth, D.B. (2005), URBAN IMPACTS ON PHYSICAL STREAM CONDITION: EFFECTS OF SPATIAL SCALE, CONNECTIVITY, AND LONGITUDINAL TRENDS1. JAWRA Journal of the American Water Resources Association, 41: 565-580. [doi:10.1111/j.1752-1688.2005.tb03755.x](doi:10.1111/j.1752-1688.2005.tb03755.x)

### The Lab Assignment

This week’s assignment is to calculate basic descriptive statistics and environmental metrics for two rivers with similar climate and drainage areas.  Do this by reading the two files into you Python code, checking for gross errors, clipping the two datasets to a consistent time period, and calculating the prescribed statistics and metrics.  

1. Use the files **TippecanoeRiver_Discharge_03331500_19431001-20200315.txt** and **WildcatCreek_Discharge_03335000_19540601-20200315.txt** provided with this repository.

   - These files contain daily discharge in cubic feet per second (cfs) for a single USGS gaging station.
   - Data file is white space delimited.
   - Column order and units are provided in the file header.
     
2. Modify the Python script template called program-09.py to complete this assignment.  The template contains code defining function names and input/output parameters, as well as comment text describing what each function should accept as parameters, return as variables, and functionally what each function should do.  **DO NOT** rename the python script, and **DO NOT** change the name or order of the parameters being sent to or from each function.  The template defines functions that the autograder program is going to import and evaluate.  Changing the program name or the function definitions, will cause the autograder to fail even if your code "works" for you.  

2. Modify the Python script template called program-09.py so that it does the following:

   - Imports the entire file in as a DataFrame, using date as the index.
   - Removes `No Data` values (defined as -999 in this file).
   - Completes the following data quality checks:
     - **Check 1:** Check for gross errors: 0 ≤ P ≤ 25; -25≤ T ≤ 35, 0 ≤ WS ≤ 10.
     - **Check 2:** Swap Tmax and Tmin when Tmax is less than Tmin.
     - **Check 3:** Check for temperature range greater than 25°C
   - Where a check is failed, replace the value with NaN.
   - Record the number of data points replaced for each of the three check types.
   - Plot each dataset before and after correction has been made.
     - Use a single set of axis for each variable, and
     - provide a legend that indicates which variable is the original and which is after quality checking.
   - Write data that has passed the quality check into a new file with the same format as the input data file.
   - Output information on failed checks to a separate Tab delimited file that can be imported into your Metadata file.

3. Be sure that the script has a complete header comment block, appropriate in-line comments, and runs without intervention relative to where the datafile is stored in the repository.

4. Create a metadata file called **METADATA.pdf** using Word, OpenOfiice or another document editor.  The metadata file shold contain the following information:

   - Name of the program, name of the program creator and a short decription of what the program does.
   - Description of the data quality checks performed and how they influenced the contents of the file.
   - Table with the number of corrections made for all three checks (should be properly referenced when discussing how data quality checks influenced the contents of the file \[see previous bullet\]). 
   - Plots for each variable before and after quality checking (these should include descriptive captions, and be properly referenced from the text). 

#### What to turn in...

The following should be included in your GitHub repository:

1. A working program called **program-09.py**, which conforms to the template provided with the original repository.

2. The original data file, **DataQualityChecking.txt**, provided with the repository.

3. The output table file from the program.

4. A metadata file called **METADATA.pdf**.

5. Put your input file, output files, and processing script in the assignment repository and push to GitHub. 

6. The instructor will follow-up with an invivtation to submit the assignment through GradeScope.  Follow the provided instructions to submit the assignment using GitHub.  The AutoGrader will return a report on whether the submitted code met the performance checks.  If errors are found, fix the code, and resubmit.

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
