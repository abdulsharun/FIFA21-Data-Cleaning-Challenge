# FIFA21 Data Cleaning Challenge

![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/FIFA21-LOGO-1080x609.jpg)

## Introduction

In March 2023, I participated in a challenge to clean FIFA21 messy data into usable format ready for analysis. The data contains information about players like name, position, team, country, etc. The data contains has 18,789 rows and 77 columns with special characters, irrelevant data and discrepancies. 

I used Microsoft Power Query to perform the following tasks of cleaning and wrangling data:

- correcting incorrect data types
- removing irrelevant data
- removing duplicates
- dealing with missing values
- correcting wrong calculations across rows and columns
- renaming columns

## Loading The Data 
To load the dataset with MS Power Query, I used UTF-8 encoding to get rid of the special characters before other cleaning tasks.

### Special Characters

   |Special character Before  | Special character After            |                                 
  ---------------------------:|:-----------------------------------
  ![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/fifa-us-ascii-encoding.png) | ![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/fifa-unicode-encoding.png)
  
## Data Transformation
After loading the data, I realized that there is need to clean (remove=ing all controls characters like tabs, end of lines) and trim (removing trailing and leading white spaces) from the dataset.
   |Before Clean and Trim | After Clean and Trim           |                                 
---------------------------:|:-----------------------------------
![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/before-clean-and-trim.png) | ![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/after-clean-and-trim.png)

Because each column has its perculiar problem, I used different techniques to clean each columns.
Here are the steps I followed to clean the data.
