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
After loading the data, I realized that there is a need to clean (removing all controls characters like tabs, end of lines) and trim (removing all trailing and leading white spaces) from the dataset.
   |Before Clean and Trim | After Clean and Trim           |                                 
---------------------------:|:-----------------------------------
![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/before-clean-and-trim.png) | ![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/after-clean-and-trim.png)

Then I checked for duplicates and found that the dataset has no duplicate values. I then removed all unwanted columns like **photo_url** which contains url to the photo of each player, **name** column because there is another column that contains the full name of the player.

Because each column has its perculiar problem, I used different techniques to clean each columns.
Here are the steps I followed to clean the data.

## ID, Name and LongName
I changed ID column data type to text because there is no need to aggregate the column (it is the unique identifier of each player). I deleted the **Name** column because the **LongName** column contains similar and more comprehensive information. I then renamed the **LongName** column to **PlayerName**.

   |ID, Name & LongName Before | ID, Name & LongName After         |                                 
---------------------------:|:-----------------------------------
![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/id-name-longname-before.png) | ![alt_text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/id-name-longname-after.png)

## Age, OVA & POT
The **Age** column represents the age of the player in text format, thus aggregation can't be done. Thus, I changed the data type to numeric so that aggregation can be done on it. 

The **OVA** column represents players overall analysis or rate in percentage. I renamed the column to **OverallAnalysis** for easy understanding, divide the column by **100**, and changed the data type to percentage. This accurately captured each player's overall analysis in percentage.

The **POT** column represents players potential in percentage. I renamed the column to **PlayerPotential** for easy readability, divide the column by **100** and changed the data type to percentage.
   |Age, OVA & POT Before | Age, OVA & POT After         |                                 
---------------------------:|:-----------------------------------
![age-ova-pot-before](https://user-images.githubusercontent.com/119185772/229858729-ed8bd357-7a58-4ca3-b43e-1af59340a260.png) | ![age-ova-pot-after](https://user-images.githubusercontent.com/119185772/229858934-04ecc4f0-5430-49c7-8c9d-7b1f383fe25b.png)



