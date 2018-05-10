# Mean-Ceramic-Date-and-Error-Estimation
Script for calculating mean ceramic dates based on tabular data. This script also estimates sampling error using a bootstrapping procedure.

Mean Ceramic Dates:
The mean ceramic date (MCD) of an assemblage is a point estimate of the occupation of a site calculated based on the frequency and date range of types present, most often used in historic archaeological contexts. The MCD is calculated by multiplying the number of sherds of a given type by the mid-point of the date range for that type (based on absolute dates or the known production interval), summing those values for all types, and then dividing by the total ceramic count (South 1977). 

The script provided here also uses a bootstrapping procedure to estimate the error (confidence interval) associated with a given mean ceramic date. For each site, 1,000 bootstrapped replicates are created by resampling with replacement from the original data. The sample sizes for each row are held constant, equal to the total number of sherds in that row in the original data and with the probability of drawing each ceramic type determined by the actual proportions of that type in the observed sample. MCDs are then calculated for each of these bootstrapped replicates to provide a means of assessing sampling error associated with the original MCD. The script returns the upper and lower 95% confidence interval estimates associated with each MCD. It is important to note that, because this procedure uses the original type frequency as the probabilistic basis for creating replicate data sets, sites with only a single type will always return only a single date.

This document provides a brief overview of the mcd.R script which can be used to calculated mean ceramic dates from two-way tables. This script is based on a program originally written by Keith Kintigh as part of the Tools for Quantitative Archaeology program suite (ARRANGE). 

File Format:
This script is designed to use the *.csv (comma separated value) file format. 

Table Format:
Two tables are required to run this script. The first table should be formatted with each of the samples/observations as rows and each of the types/wares to be included as columns. The first row of the spreadsheet should be a header that labels each of the columns. The first column should contain the name of each unit (i.e., level, unit, site, etc.). Row names may not be repeated. All of the remaining columns should contain counts by type. This analysis will not work if there are missing data in any rows or columns, so samples with missing data should be removed before running the script. Also, the script may not work with site or type names including any of the following characters (, ' "/*). 

A second table of types along with associated dates is also required. The first row of this table should consist of the type name (note that type names must exactly match those used as columns in the previous table). The second and third rows should consist of the beginning and ending dates (only numeric values) of each type. The first row of the table should be a header that labels each of the columns. This second table may contain types not represented in the first table, although this may make calculations take slightly longer. 

NOTES FOR USING THIS SCRIPT WITH B.C.E. DATES:
In order for this script to work correctly when using B.C.E. dates, enter those dates as negative numbers in the mcd_type.csv file. For example, 4000 B.C.E. would be -4000 and so on.

Requirements for Running the Script:
In order to run this script, you must install the R statistical platform. No other packages are required.

Running the Script:
The first step for running the script is to place the script file "mcd.R" and the data files ("mcd_data.csv" and "type_dates.csv") in the working directory of R. To change the working directory, click on "File" in the R window and select "Change dir", then simply browse to the directory that you would like to use as the working directory. Next, to actually run the script, type the following line into the R command line:

source('mcd.R')

At this point, the script will create a new table of all calculated MCDs as well as the upper (95high) and lower (95low) 95 % confidence intervals (mcd_out.csv). This file will be placed in the R working directory. If you run the script again, this output file will be overwritten automatically.

Reference

South, Stanley A.
1977 Method and Theory in Historical Archaeology. Academic Press, New York.
