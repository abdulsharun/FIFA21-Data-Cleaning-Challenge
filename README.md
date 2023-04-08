# FIFA21 Data Cleaning Challenge

![alt text](https://github.com/abdulsharun/FIFA21-Data-Cleaning-Challenge/blob/main/FIFA21-LOGO-1080x609.jpg)

## Introduction

In March 2023, I participated in a challenge to clean FIFA21 messy data into usable format ready for analysis. The data contains information about players like name, position, team, country, etc. The data has 18,789 rows and 77 columns with special characters, irrelevant data and discrepancies. 

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
![fifa-us-ascii-encoding](https://user-images.githubusercontent.com/119185772/230711222-484e80ea-f412-435d-bb85-69dd165279a2.png) | ![fifa-us-ascii-encoding](https://user-images.githubusercontent.com/119185772/230711231-d9e8f535-c627-451a-bd9e-0f6d921c723e.png)

## Data Transformation
After loading the data, I realized that there is a need to clean (removing all controls characters like tabs, end of lines) and trim (removing all trailing and leading white spaces) from the dataset.
   |Before Clean and Trim | After Clean and Trim           |                                 
---------------------------:|:-----------------------------------
![before-clean-and-trim](https://user-images.githubusercontent.com/119185772/230711273-cd0e07a0-7164-4030-9283-e00c332cce27.png) | ![after-clean-and-trim](https://user-images.githubusercontent.com/119185772/230711279-bc616a46-6181-4bf7-bbe1-dce1a30913fb.png)

Then I checked for duplicates and found that the dataset has no duplicate values. I then removed all unwanted columns like **photo_url** which contains url to the photo of each player, **name** column because there is another column that contains the full name of the player.

Because each column has its perculiar problem, I used different techniques to clean each columns.
Here are the steps I followed to clean the data.

## ID, Name and LongName
I changed ID column data type to text because there is no need to aggregate the column (it is the unique identifier of each player). I deleted the **Name** column because the **LongName** column contains similar and more comprehensive information. I then renamed the **LongName** column to **PlayerName**.

   |ID, Name & LongName Before | ID, Name & LongName After         |                                 
---------------------------:|:-----------------------------------
![id-name-longname-before](https://user-images.githubusercontent.com/119185772/230711308-d36da9db-a2ca-45e2-93e9-28e92f28b4a7.png)
 | ![id-name-longname-after](https://user-images.githubusercontent.com/119185772/230711326-6637f621-e862-4f11-bf79-f5403604d805.png)

## Age, OVA & POT
The **Age** column represents the age of the player in text format, thus aggregation can't be done. Thus, I changed the data type to numeric so that aggregation can be done on it. 

The **OVA** column represents players overall analysis or rate in percentage. I renamed the column to **OverallAnalysis** for easy understanding, divide the column by **100**, and changed the data type to percentage. This accurately captured each player's overall analysis in percentage.

The **POT** column represents players potential in percentage. I renamed the column to **PlayerPotential** for easy readability, divide the column by **100** and changed the data type to percentage.
   |Age, OVA & POT Before | Age, OVA & POT After         |                                 
---------------------------:|:-----------------------------------
![age-ova-pot-before](https://user-images.githubusercontent.com/119185772/229858729-ed8bd357-7a58-4ca3-b43e-1af59340a260.png) | ![age-ova-pot-after](https://user-images.githubusercontent.com/119185772/229858934-04ecc4f0-5430-49c7-8c9d-7b1f383fe25b.png)

## Contract Column
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

4. Lastly, I subtracted **ContractStarts** from **ContractEnds** to get **ContractDuration(Years)**; a new column that shows numbers of years a *contracted* player spent in a team. And the cleaned columns are shown below.

![contract-agreement-final](https://user-images.githubusercontent.com/119185772/229865191-dca2709b-4414-47f9-b250-bfda8fdbf6b6.png)

## Weight & Height
The **Weight** column contains data in two units (kg & lbs). In order to make the column consistent, I converted all weights to **kg** using the following steps:
1. I splitted the weight column by ***Digit to Non-Digit*** to get the numbers and units in different columns; **Weight.1** and **Weight.2** respectively.
2. I created a multiplier column that has **0.454** if the **Weight.2** is **lbs** and **1** if it is **kg**.
3. I multiplied the initial column by the multiplier column to get the weight in kg.
4. I renamed the column to **Weight(Kg)**.

|Cleaning the weight column|                                 
|---------------------------:|
|![weight-cleaning](https://user-images.githubusercontent.com/119185772/230706108-adcf2c35-1746-446a-bd48-efc50b6c8d1b.png)|

The **Height** column contains data in two formats (170cm and 5'7") which makes it inconsistent. I cleaned this column by using the following steps:
1. I added a **multiplier** column to convert inches to cm by mulplying the column by 2.54.

![multiplier2 54](https://user-images.githubusercontent.com/119185772/230707622-fc59b485-60b2-4500-b19c-d664b5f892cf.png)

2. I splitted the column on **'** delimeter to obtain the feet and inches in different columns; **Height.1** and **Height.2**.
3. I replaced all null values in **Height.2** with **0** because I will perform addition with this column later. I renamed this column to **addition**.
4. I created a multiplier column to convert all values in feet in **Height.1** to inches as shown below.

![multiplier12](https://user-images.githubusercontent.com/119185772/230707631-53022427-3531-4abf-bc73-392109cc5855.png)

5. I replaced **cm** in **Height.1** with space and converted the data type to numeric.

![replaced-cm](https://user-images.githubusercontent.com/119185772/230707647-60de5dcc-d987-4f31-b0c2-6361cc18918e.png)

6. I then multiplied the **Height.1** with **multiplyby12**, then added the **addition** column.
7. Lastly I multiplied the **Height.1** with **multiplier** to obtain the final value in **cm** and renamed the column to **Height(cm)**.

|Weight & Height Before | Weight & Height After    |                                 
---------------------------:|:-----------------------------------
![weight-height-before](https://user-images.githubusercontent.com/119185772/230707696-51c01c53-0b4d-4473-9b0c-d067a379e963.png) | ![weight-height-after](https://user-images.githubusercontent.com/119185772/230707706-2849b5ff-cda3-47ad-8e3d-986591efcce2.png)

## Loan Date End
This column was observed to have some empty cells. But after cross-checking the data, I realised that the the empty corresponds to players that are not on loan in the currrent clubs. So, I replaced all empty cells with **Not on loan**.

|Loan Date End Before | Loan Date End After    |                                 
---------------------------:|:-----------------------------------
![loan-date-before](https://user-images.githubusercontent.com/119185772/230708397-7b7090d0-d7ed-43e6-9004-33b02844ac87.png) | ![loan-date-after](https://user-images.githubusercontent.com/119185772/230708412-f7215046-f627-42ad-9015-128a55a7d810.png)

## Value, Wage & Relause Clause
These columns have numerical data in the format that cannot be used for aggregation like €138.4M and €138.4K. Thus I cleaned the columns by:
1. Splitting the columns to remove the € symbol and renaming the columns appropriately.
2. Creating multiplier columns to take care of the **M**'s and **K**'s.
![multiplier-vwrc](https://user-images.githubusercontent.com/119185772/230709331-601e602d-f80c-494a-9ec2-4d9da48810ac.png)

3. Removing the **M**'s and **K**'s and converting the columns to numeric.
4. Multiplying the columns by their individual multiplier columns to get a consistent result.
5. Converting the columns to currency.

| Value, Wage & Relause Clause Before | Value, Wage & Relause Clause After    |                                 
---------------------------:|:-----------------------------------
![value-wage-rc-before](https://user-images.githubusercontent.com/119185772/230709357-fa7cfb2b-4172-4adc-81ea-e6d38dfe4336.png) | ![value-wage-rc-after](https://user-images.githubusercontent.com/119185772/230709368-3d0c9101-d33d-40aa-8e20-626142c11271.png)

## Weak Foot, Skill Moves & Injury Ratings
These columns are named **W/F**, **SM** & **IR** in the dataset which represent Weak Foot Rating, Skill Moves Rating & Injury Rating. They contained the symbol ★. Thus I removed the symbol and renamed the columns for easy readability and understanding.

| Weak Foot, Skill Moves & Injury Ratings Before | Weak Foot, Skill Moves & Injury Ratings After    |                                 
---------------------------:|:-----------------------------------
![wr-sm-ir-before](https://user-images.githubusercontent.com/119185772/230710327-8f6a0603-ab3e-4ded-bb3b-981c7dcd8eb3.png) | ![wr-sm-ir-after](https://user-images.githubusercontent.com/119185772/230710235-2a90298e-dd2f-4650-a86f-452fcd541c91.png)

## Other columns
Apart from the columns explained above, there are other columns in the dataset. Most of these columns only have the wrong dataype, so I changed the datatypes to the appropriate ones.

| Other Columns Before | Other Columns After    |  
---------------------------:|:-----------------------------------
![other-columns-before](https://user-images.githubusercontent.com/119185772/230710983-82e0ced9-b69e-4f36-bef7-d498c99086f9.png) | ![other-columns-after](https://user-images.githubusercontent.com/119185772/230711004-02355453-712f-43aa-9fb1-f75b72024501.png)

## Conclusion
In this project, I was able to use Power Query to clean FIFA21 data that contains inconsistent information, wrong data types, missing values and columns. The data is now cleaned and ready for analysis. It is fair to say that I have learnt some concepts of data cleaning by joing this challenge. I look forward to analysing this data and doing more projects to solidify what I have learnt. 

Thank you for reading and I anticipate your feedback and recommendations on how to make this project better.
