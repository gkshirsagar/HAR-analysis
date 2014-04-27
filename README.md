HAR-analysis
============

Clean-up and collate data contained in several tables recording detailed parameters on Human Activity Recognition using smartphones.

## Source Files
* `CodeBook.md`: Describes the variables in the data and transformations done to tidy up the data.
* `README.md`: This file.
* `run_analysis.R`: An R script that runs on the data, analyzes it and tidies it up.

## Dependencies
The `run_analysis.R` script depends mostly on the `base` package of R and some functions from the `reshape2` package.
`reshape2` should be installed by default in your R installation, but if it isn't installed, please install it using `install.packages("reshape2")`.

## Running
1. Download and unzip the dataset (should be titled as `getdata-projectfiles-UCI HAR Dataset.zip`) in your working directory (in which `run_analysis.R` is present).
2. On unzipping, a directory called `UCI HAR Dataset` should be created in the working directory. It is necessary that the name of this directory be preserved as the script looks for a directory with this name for its data files.
3. In your R environment, type `source("./run_analysis.R")` to run the script.
4. After performing the analysis, if successful, the script should produce a tidied up and summarized table contained in a new file called `tidydata.txt`.
5. The table created in step 4 can be opened in a text editor for viewing.
6. The table created in step 4 can also be easily imported back into R using `read.table("./tidydata.txt", header=TRUE)`.
