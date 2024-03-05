
# DATA.TABLE

# Expanding the Open-Source Ecosystem for the R data.table Package

This project, funded by the NSF under th POSE is aiming to enhance the opensource surrounding the R data.table package.

data.table is a powerful R package that provides an enhanced version of the traditional data.frame object. It is designed for efficient data manipulation, particularly for large datasets.

 ## Objective
 
 1. Documentation Enhancement
 2. Community Engagement
 3. Bug fixes and Performance Regression Optimization
 4. Package Extension

## My Expected Outcomes

A more stable and optimized data.table package, with improved performance and usability.

## Performance Regression Analysis in the data.table Package

## Description:
This repository aims to investigate performance regressions in the data.table package by examining its history, creating relevant performance tests, and using atime to analyze the performance of different code branches (before regression, regression, fix regression). Additionally, it provides a GitHub Action called r-asymptotic-testing that allows you to perform asymptotic testing on your data.table repository package upon every push/pull request.

## User Guide

I have a [presentation](https://github.com/DorisAmoakohene/Data.table-Presentation) in Powerpoint which  delves into the data.table package in R, It highlights the efficiency of data.table by comparing it to other packages. The presentation also emphasizes the significance of performance testing, which was conducted using the reported issues on the data.table repository on GitHub. This testing process helped establish three distinct code branches: Regression, Before, and Fix.

# To Start:

1. To begin, conduct the atime test for the different code branches (before regression, regression, fix regression) to identify potential performance issues. [Here](https://github.com/DorisAmoakohene/Researchwork_Rdata.table/blob/main/Performance%20regression%20with%235424.Rmd) is an example of how to perform the atime test

  NB: Set up the necessary environment and dependencies, ensuring that the data.table package and the atime package are installed and loaded.

2. Generate a plot to showcase the fixes made in the data.table package using the atime package. Utilize the `atime_versions` function to track the fixes across different versions. Pass the following named arguments to `atime::atime_versions`: N, setup, expr, and the different code branches. More documentation of the atime package can be found [here](https://github.com/tdhock/atime/blob/compare-dt-tidy/man/atime_pkg.Rd). The documentation provides detailed information on how to use the atime package for performance analysis and tracking changes across different versions

3. Use the `plot` function to visually represent the execution times of the expression evaluated across different versions of the data.table package.

4. Run the GitHub Action by writing tests in `inst/atime/tests.R`. Define `test.list` as a list with names corresponding to different tests. Each element should be a list with named elements N, setup, expr, to be passed as named arguments to `atime::atime_versions`.  For further elaboration on the process of performing asymptotic time testing using the atime package, please refer to [this](https://github.com/marketplace/actions/r-asymptotic-testing)

# Example Usage

A. Provide links to the issue(s) comment(s) containing the original code(s) that reported the regression. If there are multiple issues with code exhibiting the regression, include links to each issue along with a summary of the observed symptoms in your own words.

B. Link to the pull request (PR) that caused the regression. Explain the cause of the performance regression in the data.table code using your own words.

C. Link to the PR that fixed the regression. Describe the changes made to fix the regression in your own words.

D. Provide links to your atime test code(s) and plot(s) that illustrate the performance regression and its fix. If there are multiple issues with code exhibiting regressions, include links and plots for each issue.

- R atime code file(s) 
- png atime figure file(s)

# Inputs:
- Links to the issue(s) comment(s) with the original code(s) reporting the regression.
- Link to the pull request (PR) that caused the regression.
- Link to the PR that fixed the regression.
- Links to the atime test code(s) and plot(s) illustrating the performance regression and its fix.

# Outputs:
- Visualizations of the performance regressions and fixes.
- GitHub Action report indicating the results of asymptotic testing on the data.table repository package.




## Performance Regression Analysis
# 1. 
   
   A. discusses regression: this link discusses the issue of Performance Regression with .N and := [issue5424](https://github.com/Rdatatable/data.table/issues/5424) other issues that was discussed includes [issues5366](https://github.com/Rdatatable/data.table/issues/5366) Significantly slower performance time-based rolling and [issue5371](https://github.com/Rdatatable/data.table/issues/5371)Memrecycle Performance Regression.
These issues address performance-related concerns and propose potential fixes or improvements to the data.table package
   
   B. The cause of the regression is related to the addition of the snprintf function in the assign.c.
   [CausesRegression](https://github.com/Rdatatable/data.table/pull/4491)
   
   C. The Regression was fixed by creating targetDesc function and adding snprintf in assign.c
   [Fixes Regression](https://github.com/Rdatatable/data.table/commit/e793f53466d99f86e70fc2611b708ae8c601a451)

   D.
   [link to my atime code](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/Performance%20regression%20with%235424.Rmd)

   ![Plot showing the 3 branches(Regression,Fixed and Before) of Issue#5424](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.list1.png)

   ![Plot showing the 3 branches(Regression,Fixed and Before) of Issues5366](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.list2.png)
   
   ![Plot showing the 3 branches(Regression,Fixed and Before) of Issues5371]()


  # 2.
 A. This issue reported a  performance regression when performing group computations, specifically when running R's C eval on each group (q7 and q8) in the db-benchmark, indicating a  slowness in the implementation of the code.[link to comment that reported Regression](https://github.com/Rdatatable/data.table/issues/4200)
  

 B. This is the [PR]( https://github.com/Rdatatable/data.table/pull/4558) that discusses the 
Cause of the Regression: [The regression was specifically related to the evaluation of C code within each group of data, specifically q7 and q8 in the "db-benchmark"](https://github.com/Rdatatable/data.table/issues/4200#issue-555186870)  which appears that the regression occurred during the evaluation of C code within these particular groups, indicating a performance issue or slowness in the implementation of the code.

C. Fixed:  
[The regression was fixed Regression by the addition of const int nth = getDTthreads]( https://github.com/Rdatatable/data.table/pull/4558/files)

D.
[link to my atime code](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/groupby%20with%20dogroups%20(R%20expression)%20performance%20regression%20%234200.Rmd)

![Plot showing the 3 branches(Regression,Fixed and Before) of the issues#4200]()


# 3.
A. This issue reported that when using the dt[selector, foo := bar] syntax  with an index defined, the performance of that operation can be significantly slower compared to when there is no index.[Major performance drop of keyed := when index is present #4311](https://github.com/Rdatatable/data.table/issues/4311)

B. [Causes Regression](https://github.com/Rdatatable/data.table/issues/4311
) The regression  was caused by utilizing the ":=" operator with an index present while modifying data by reference.

C. [Fixes Regression by passing shallow(dt.s4) to the isS4() function](https://github.com/Rdatatable/data.table/pull/4440)

D. [Link to my atime code showing this Regression](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/Remove%20deep%20copy%20of%20indices%20from%20shallow.Rmd)

![Plot showing the 3 branches(Regression,Fixed and Before) of the issues#4440](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.list.4440.png)


# 4. 
A. [Reported the issue : GForce optimisation could be more smart](https://github.com/Rdatatable/data.table/issues/3815)

B. The issue was reported to check the efficiency of the original code [(now = DT[, .(range_v1_v2=max(v1, na.rm=TRUE)-min(v2, na.rm=TRUE)), by=id3 ])](https://github.com/Rdatatable/data.table/issues/3815#issuecomment-1509890222)

C. This Regression is still Open

D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/GForce%20optimisation%20could%20be%20more%20smart%20%233815.Rmd)

![Plot showing the the memory and time metrics of the issue from the atime](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.list.3815.png)


# 5. 
A. [frollmax is slow on descending sequences](https://github.com/Rdatatable/data.table/issues/5923)

B. [This issue refers to the slower performance of the data.table::frollmax() function when applied to descending sequences compared to ascending sequences.](https://github.com/Rdatatable/data.table/issues/5923#issue-2104222037)

C. This issue is still Open

D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/data.table%20frollmax%20on%20descending.Rmd)

![Plot showing the the memory and time metrics of the issue from the atime](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/result.frollmax.png)


# 6. 
 A. [faster bmerge numeric and roll #5187](https://github.com/Rdatatable/data.table/pull/5187#issuecomment-1881694259)
 
 B. [The problem is trying to optimize the performance of aligning two datasets based on date values, and they are experimenting with different approaches using data frames and data tables.](https://github.com/Rdatatable/data.table/pull/5187#issuecomment-947107447)
 
 C. This PR is still Open

 D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/faster%20bmerge%20numeric%20and%20roll%20%235187.fix.Rmd)

![Plot showing the the memory and time metrics of the issue from the atime]()

 
 # 7. 
  A. [.data.table is very slow with a single integer #5636 ](https://github.com/Rdatatable/data.table/issues/5636 )
  
  B. This is issue about suggests  performance problem when using the data.table package with a single integer. The issue can be confirmed from this reported [ code snippet ](https://github.com/Rdatatable/data.table/issues/5923#issue-2104222037) 
  
  C. This issue is currently open

  D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/data.table%20is%20very%20slow%20with%20a%20single%20column%20%235650.Rmd)

![Plot showing the the memory and time metrics of the issue from the atime]()
  

 # 8.
  A. [Grouped calculations of list columns are very slow #5428](https://github.com/Rdatatable/data.table/issues/5428)
  
  B. This issue is about the slow performance of creating a list column in a [grouped calculation using the data.table package.] (https://github.com/Rdatatable/data.table/issues/5428#issue-1327797930)

  C.  This issue is still open

  D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/Grouped%20calculations%20of%20list%20columns%20are%20very%20slow%20%235428.Rmd)

![Plot showing the the memory and time metrics of the issue from the atime](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.5428.png)

  
# 9.

A.[implement frev() - base::rev() that allocates less #5885](https://github.com/Rdatatable/data.table/issues/5885)

B. [implement frev as fast base::rev alternative #5907](https://github.com/Rdatatable/data.table/pull/5907)

C. This PR was fixed by introducing an [export(frev)](https://github.com/Rdatatable/data.table/pull/5907/files)

D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/implement%20frev().Rmd)

![Plot showing the the memory and time metrics of the issue from the atime](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.result.frev.png)



# 10. 

A.[locating performance improvement in NEWS #5900](https://github.com/Rdatatable/data.table/issues/5900)

B.benchmark of this PR vs master and 1.14.0,  using 1, 2, 4, 8 threads, to measure the efficiency of gmin parallizle per group [#5916](https://github.com/Rdatatable/data.table/pull/5916)

C. Fixed by #5916 by adding this line [int *restrict ansd = INTEGER(ans);const int *restrict xd = INTEGER(x); to the code](https://github.com/Rdatatable/data.table/pull/5916/files)

D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/locating%20performance%20improvement%20in%20NEWS%20%235900.Rmd)

![Plot showing the the memory and time metrics of the issue from the atime](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.result.5900.png)



# 11.

A.Major performance drop of keyed := when index is] present#4311](https://github.com/Rdatatable/data.table/issues/4311)

B. The issue reported a significant performance drop when using the dt[selector, foo := bar] syntax on a keyed data.table when an index is present.[#4440](https://github.com/Rdatatable/data.table/pull/4440)

C. The issue was resolved by introducing a new internal function called `shallow()`. [This function avoids creating a deep copy of secondary indices, leading to improved performance.](https://github.com/Rdatatable/data.table/pull/4440/files)

D. [link to my atime code visualizing the issue]()

![Plot showing the the memory and time metrics of the issue from the atime]()



# 12.

A.[Move some setDT validation checks to C #5427](https://github.com/Rdatatable/data.table/pull/5427)

B. [setDT extremely slow for very wide input #5426](https://github.com/Rdatatable/data.table/issues/5426)

C. Fixed by 

D. [link to my atime code visualizing the issue](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/setDT%20extremely%20slow%20for%20very%20wide%20input%20%235426.Rmd)

![Plot showing the the memory and time metrics of the issue from the atime](https://github.com/DorisAmoakohene/Efficiency-and-Performance-Test.RData.table/blob/main/atime.list.5427.png)







## I utilize a GitHub Action to run my forked repository of data.table explain above. You can find the repository by [clicking here](https://github.com/DorisAmoakohene/data.table). 

![The GitHub Action generates a plot illustrating the asymptotic timing of the issues from GitHub above](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/tests_all_facet.png) 

By adding the commit id this is how the plot should look
![Example of a plot graph you should see](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/new%20action/tests_all_facet.png)

see other plot [HERE](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/tree/main/new%20action)




# Efficiency of the Data.Table and other Packages
This aspect of the project aims to enhance the atime compare-data.table-tidyverse vignette by conducting an efficiency analysis of data.table and popular R packages such as Polar, collapse, dplyr, baseR, and Reshape. 

The objective is to provide users with optimized data manipulation techniques and enable them to make informed choices for efficient data processing within the R ecosystem."

This is a link to all the [codes](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/vignette%20atime%20data.t.Rmd) performing this analysis

## Plot

In this file, I conducted a comparison between data.table's CSV writing capabilities and other R packages such as readr, arrow, polars, and BaseR. The objective was to assess the performance and efficiency of these packages when it comes to writing CSV files in R
1. ![Writing CSV files ](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/gg.write.png) 

2. ![Reading CSV Files](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/gg.read.png) 

In this analysis, I  examined the efficiency of summarizing data by group using data.table and various other packages including dplyr, stats, summarytools, psyc, and plyr. The goal was to compare the performance and effectiveness of these packages in performing group-wise data summarization tasks.

3. ![Summarizing by Group](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/ml.gg.png)

4. ![Summarize by group, expanded](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/ml.exp.gg.png)


Conducted a comparison of data reshaping techniques between data.table and other packages such as Stats Reshape and tidyr. The focus was on evaluating the efficiency and effectiveness of these packages in transforming data between wide and long formats, enabling users to make informed choices based on their specific data reshaping needs.

5. ![Reshaping wide to long ](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/ml.reshape.png)

6. ![Reshaping Long to wide](https://github.com/DorisAmoakohene/Efficiency-and-Preformance-Test.RData.table/blob/main/ml.wide.png)

This shows the comparison of creating data frames in R using data.frame, data.table and tibble in dplyr

7. ![Creating dataframe](https://github.com/DorisAmoakohene/Researchwork_Rdata.table/blob/main/ml.create.png)
