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

**Contract Column**
The **Contract** column contains inconsistent data as shown below:
![contract-before](https://user-images.githubusercontent.com/119185772/229860330-9e16b27c-0a35-4e4c-965b-d64d52002428.png)

I cleaned the column by using the following steps:
1. I created an **Agreement** column which will represent whether a player is on **Contract**, **On Loan** or **Free**. 
![agreement-before](https://user-images.githubusercontent.com/119185772/229860962-9006d7c9-9728-4bc0-ba30-b7e2d05a6bf5.png)
2. I splitted the **Contract** column on **~** delimeter and renamed the two columns to **ContractStarts** and **ContractEnds**.
3. I replaced the empty cells in both columns with **null** to avoid errors. 

|Splitting Contract Contract | Replacing empty cells with null     |                                 
---------------------------:|:-----------------------------------
![contract-split](https://user-images.githubusercontent.com/119185772/229862366-66dd72a3-1bb4-483f-af50-9333100dad61.png) | ![contract-replace-nulls-rename-columns](https://user-images.githubusercontent.com/119185772/229862425-699a49b0-f876-4ab0-85df-fefa5f499e33.png)

