# Nashville Traffic Accidents Analysis  

## Project Overview  
This project analyzes a dataset of traffic accidents in Davidson County, Nashville, using spreadsheet functions to extract insights. The dataset was sourced from [Nashville Open Data](https://data.nashville.gov/datasets/1df26ca05f3f407e95ab5a4fc013eab7_0/explore).  

The analysis covers various aspects, including the total number of accidents, trends over time, collision types, and accident distribution based on factors such as time of day, day of the week, and road conditions.  

## Dataset  
The dataset consists of multiple sheets:  
- **Question** – Question + Answer keys
- **Analysis** – Results of calculations and insights  
- **Accidents** – Raw accident data
- **Zero Car Crashes** – Filtered cases with zero vehicles involved   
- **Collision Types** – Lookup table for collision type codes
- **Weather Types** – Lookup table for weather type codes
- **Illumination Types** – Lookup table for illumination type codes
- **Harmful Types** – Lookup table for harmful type codes


---

## Key Questions & Formulas  

### 1. How many total accidents are contained in this dataset?  
```excel
=COUNT(Accidents!A:A)
```

### 2. What are the earliest and latest records that appear in this dataset?  
To count earliest record:  
```excel
=MIN(Accidents!B:B)
```
To count latest record:  
```excel
=MAX(Accidents!B:B)
```

### 3-a. Create a new column to the right of the "Number of Motor Vehicles" column called "Single or Multiple". 
```excel
=IFS(G2<1,"None",G2=1,"Single",G2>1,"Multiple")
```

### 3-b. Are there any rows that involved zero vehicles? How many? Make sure that your formula accounts for these cases.  
```excel
=COUNTIF(Accidents!G:G, "0")
```

### 3-c. Investigate the rows that have zero vehicles using the FILTER function in the "Zero Car Crashes" sheet.
```excel
=FILTER(Accidents!A1:Y218320, Accidents!G1:G218320=0, 0)
```

### 3-d. What percentage of crashes are single-car?
```excel
=COUNTIF(Accidents!G:G, "1")/Analysis!B1
```

### 4. How many accidents occurred which are hit and run and had at least one injury?  
```excel
=COUNTIFS(Accidents!K:K, TRUE, Accidents!I:I, ">0")
```

### 5-a. What is the overall average number of injuries?    
```excel
=AVERAGE(Accidents!I:I)
```

### 5-b. Are there any rows that involved zero vehicles? How many? Make sure that your formula accounts for these cases.      
To count number of Crashes:  
```excel
=COUNTIF(Accidents!M:M,A2)
```
To count average injuries:  
```excel
=E2/C2		
```
To count total injuries:  
```excel
=SUMIFS(Accidents!I:I,Accidents!M:M,A2)	
```

### 6. Add four new columns, Month, Year, Hour, and Weekday to the right of the Date and Time column.       
To create a month:  
```excel
=TEXT(B3,"mmmm")
```

To create a year:  
```excel
=TEXT(B2,"yyy")	
```

To create a hour:  
```excel
=TEXT(B2,"hhh")
```

To create a weekday:  
```excel
=TEXT(B2,"dddd")
```

### 7. Fill in the Hour table in the Analysis spreadsheet to find the number of accidents that occurred for each hour of the day. 
```excel
=COUNTIF(Accidents!E:E, Analysis!A15)
```

### 8. Do the same for the year and day of the week.   
For the year:
```excel
=COUNTIF(Accidents!D:D, Analysis!D15)
```
For day of the week:  
```excel
=COUNTIF(Accidents!F:F, Analysis!D26)
```

### 9. Add a column to the right of the Collision Type Code called "Collision Type". 
```excel
=VLOOKUP(M2,'Collison Types'!$A$2:$B$11, 2, FALSE)
```

### 10. Which interstate has the most accidents between I-24, I-40, I-65, and I-440?  
```excel
=COUNTIF(Accidents!R:R,CONCAT("*",A41,"*"))
```

---

## Tools & Functions Used  
- **Spreadsheet functions:** `COUNTIF`, `SUMIFS`, `AVERAGE`, `VLOOKUP`, `TEXT`, `FILTER`, `IFS`, `CONCAT`  
- **Data filtering and conditional logic** for identifying key trends  
- **Charts** for visual representation  

## How to Use  
1. Open the spreadsheet and review the **Accidents** sheet.  
2. Navigate to the **Analysis** sheet to explore results.  
3. Use the **Collision Types** and **Zero Car Crashes** sheets for reference.  
