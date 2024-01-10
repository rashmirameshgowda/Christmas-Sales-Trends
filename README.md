
# Christmas Sales & Trends

This report is built as to directly answer the questions that pop-up while looking at the dataset.

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 5 : Replaced values in 'OnlineOrderFlag' with Online and Offline for 1 and 0 respectively. 
- Step 6 : Created 'bins' for 'Time' and 'Age' columns to categorize the data for ease.
- Step 7 : Derived AgeCategory column from 'Age Bins' column. (dax below)
- Step 8 : Derived Day column Date column. (dax below)


### DAX Columns

AgeCategory = IF('Onyx Data -DataDNA Dataset Chal'[AgeBins] = 10, "18-20", IF('Onyx Data -DataDNA Dataset Chal'[AgeBins] = 20, "20-30", IF('Onyx Data -DataDNA Dataset Chal'[AgeBins] = 30,"30-40", IF('Onyx Data -DataDNA Dataset Chal'[AgeBins] = 40, "40-50", IF('Onyx Data -DataDNA Dataset Chal'[AgeBins] = 50, "50-60", IF('Onyx Data -DataDNA Dataset Chal'[AgeBins] = 60, "60-70", IF('Onyx Data -DataDNA Dataset Chal'[AgeBins] = 70, "70-80")))))))

Day = FORMAT('Onyx Data -DataDNA Dataset Chal'[Date], "dddd")
  
### DAX Measures :

ReturnCount = COUNTROWS(FILTER('Onyx Data -DataDNA Dataset Chal', 'Onyx Data -DataDNA Dataset Chal'[ReturnFlag] = True))

Avg Return Rate = DIVIDE('Onyx Data -DataDNA Dataset Chal'[ReturnCount], COUNT('Onyx Data -DataDNA Dataset Chal'[TransactionID]))

Avg Transaction per Customer = (COUNT('Onyx Data -DataDNA Dataset Chal'[TransactionID]))/(DISTINCTCOUNT('Onyx Data -DataDNA Dataset Chal'[CustomerID]))

GiftsCount = COUNTROWS(FILTER('Onyx Data -DataDNA Dataset Chal', 'Onyx Data -DataDNA Dataset Chal'[GiftWrap] = True))

Gifts % = DIVIDE('Onyx Data -DataDNA Dataset Chal'[GiftsCount], COUNT('Onyx Data -DataDNA Dataset Chal'[TransactionID]))

Product Avg Return Rate = DIVIDE('Onyx Data -DataDNA Dataset Chal'[ReturnCount], COUNT('Onyx Data -DataDNA Dataset Chal'[Category]))

### The report consists of 3 tabs :

### Sales Trend

![SalesTrend](https://github.com/rashmirameshgowda/Christmas-Sales-Trends/assets/153609997/dc48c051-5cde-4fde-bae3-034b3ac8e31c)

### Returns

![Returns](https://github.com/rashmirameshgowda/Christmas-Sales-Trends/assets/153609997/3b54dbeb-d374-43d7-8892-7ca364be6719)

### Revenue

![Revenue](https://github.com/rashmirameshgowda/Christmas-Sales-Trends/assets/153609997/95ffe1e3-e3b3-4c66-b8b3-325768ca23c7)



