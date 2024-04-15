[Pandas Documentation](http://pandas.pydata.org/)

# **Data Wrangling**


### **Pre-Processing Data in Python**
- Data Pre-Processing: The process of converting or mapping data from the intial "raw" form into another format, in order to prepare the data for further analysis.
    - **Also known as:**
        - Data Cleaning
        - Data Wrangling
- Steps:
    1. Identifying and handling missing values
    2. Data Formatting
    3. Normalizing Data
        - Centering
        - Scaling
    4. Data Binning
    5. Turning Categorical Values to Numeric Values



Things to Remember:
- Each row in a data set represents a sample
- You access a column by specifying the name of the column
    - df["column_name_1"]
    - df[["column_name_1","column_name_2",...]]
- You can manipulate a column in Python
    - You can add a value to each item in a column
        - df["column_name_1"] = df["column_name_1"] + 1
        - This adds 1 to the each value in the column
        
        
        
# **Dealing with Missing Values in Python**
- Missing values occur when no data value is stored for a variable (feature) in an observation
- Could be represented as "NaN", "?", "N/A", 0 or just a blank cell
- How to deal with missing data
    - Check with the data collection source
        - Evaluate for missing Values
        - **You can use two methods to detect missing data**
            - **.isnull()**
            - **.notnull()**
            - **i.e. missing_data = df.isnull()**
            - **missing_data.head(5)**
    - Count missing values in each column
        - Use a for loop in Python
        - Remember which is True and Which is False
        - In the body of the loop, the method ".value_counts()" counts the number of "True" values.
            - **for column in missing_data.columns.values.tolist():**
                - **print(column)**
                - **print(missing_data[column].value_counts())**
                - **print("")**
    - To see which values are present in a particular column, we can use the **.value_counts()** method
        - **df["column_name"].value_counts()** 
        or
        - **df["column_name"].value_counts().idxmax()** to calculate the most common type automatically
    - Drop the missing values
        - Drop the variable (column)- (axis=1)
        - Drop the data entry (sample)- (axis=0)
            - do this if there are not a lot of missing values
    - Replace the missing values
        - **use the .replace(A,B, inplace = True) function**
            - **i.e. df["column_name"].replace("?",np.nan, inplace = True)**
        - Replace value with an average (of similar datapoints)
            - for numerical data
            - calculating the mean
                - **avg_column_name = df["column_name"].astype("float").mean(axis=0)**
            - Replace "NaN" with the mean value
                - **df["column_name"].replace(np.nan, avg_column_name, inplace = True)**
        - Replace value by frequency
            - mode
            - for categorical data that cannot be averaged
        - Replace value based on other functions
            - if you know something about the data and can make an educated guess
        - less accurate
    - Leave it as missing data
    
    
### **How to Drop Missing Values in Python**
- Use dataframes.dropna():
    |highway-mpg|price|
    |:---------:|:---:|
    |...|...|
    |20|23875|
    |22|NaN|
    |29|16430|
    |...|...|
    
    
- axis=0 drops the entire row
- axis=1 drops the entire column
  
  
- **df.dropna(subset="price"], axis=0, inplace = True)**
    |highway-mpg|price|
    |:---------:|:---:|
    |...|...|
    |20|23875|
    |29|16430|
    |...|...|   
        - note: setting  inplace = True  allows the modification to be done on the data set directly. This writes the result back into the dataframe.
        - df.dropna(subset=["price"], axis=0   does not change the dataframe. You need to make inplace = True
        - don't forget to reset the index if you drop rows
            - **df.reset_index(drop=True,inplace=True)**


### **How to Replace Missing Values in Python**
- Use dataframe.replace(missing_value,new_value):


|normalized-losses|make|
|:----------------|:---|
|...|...|
|164|audi|
|164|audi|
|**NaN**|audi|
|158|audi|
|...|... |


1. Calculate the mean of the column
    - **mean** = df["normalized-losses"].mean()
2. Use the method  **.replace**  to specify the value we would like replace the value
 - df["normalized-losses"].replace(np.nan,**mean**)


# **Data Formatting**
- Data is usually collected from different places and stored in different formats
- Data Formatting is bringing data into a common standard of expression which allows users to make meaningful comparisons

**Non-Formatted Data:**
- confusing
- hard to aggregate
- hard to compare
|City|
|----|
|N.Y.|
|Ny|
|NY|
|New York|

**Formatted Data:**
- more clear
- easy to aggregate
- easy to compare
|City|
|----|
|New York|
|New York|
|New York|
|New York|


### **Applying Calculations to an Entire Column**
- Convert "mpg" to "L/100km" in Car dataset

|city-mpg|
|--------|
|21|
|21|
|19|
|...|

to 

|city-L/100km|
|--------|
|11.2|
|11.2|
|12.4|
|...|
    
        
**df["city-mpg"] = 235/df["city-mpg"]**

**df.rename(columns={"city_mpg": "city-L/100km"}, inplace=True)**


### **Incorrect Data Types**
- There are many data types in Pandas
    - Objects: "A","Hello",...
    - Int64: 1,3,5
    -Float64:2.123,632.31,0.12
- Sometimes the wrong data type is assigned to a feature
    - df["price"].tail(5
 
 
Incorrect Data Type:
|   |     |
|---|-----|
|200|16845|
|201|19045|
|202|21485|
|203|22470|
|204|22625|

Name: price,dtype: object





**To *identify* data types:**
- Use dataframe.dtypes() 


**To *convert* data types:**
- Use dataframe.astype() to convert data type

Example: Convert data type to integer in column "price"
- df["price" = df["price"].astype("int")



### **Data Normalization in Python**
**Data not Normalized**
- "age" and "income are in different ranges
- hard to compare
- in linear regression, the attribute "income" will influence the result more due to its larger value

|age|income|
|---|------|
|20|100000|
|20|20000|
|40|500000|

**Normalized Data**
- similar value range

|age|income|
|---|------|
|0.2|0.2|
|0.3|0.04|
|0.4|1|


**Several Approaches for Normalization**
1. Simple Feature Scaling
    - new_ value = old_value / max_value
    
2. Min-Max
    - new_value = old_value - min_value / max_value - min_value
    
3. Z-score (Standard Score)
    - new_value = old_value - average / standard deviation


### **Note:**
    - Data Standardization
        - You usually collect data from different agencies in different formats. (Data Standardization is also a term for a particular type of data normalization where you subtract the mean and divide by the standard deviation.)
        - Standardization is the process of transforming data into a common format, allowing the researcher to make the meaningful comparison.
        Example:
            - Transform mpg to l/100km:
            In a data set, the fuel consumption columns "city-mpg" and "highway-mpg" are represented by mpg (miles per gallon)unit. Assume you are developing an application in a country that accepts the fuel consuption with L/100km standard
            you will need to apply DATA TRANSFORMATION to transform mpg into L/100km.
            Use the formula for unit conversion: L/100km = 235/mpg
            You can do many mathematical operations directly using Pandas.
            Df['city-L/100km'] = 235/df['city-mpg']


### **Binning in Python**
- Binning: Grouping of values into bins
- Converts numeric into categorical variables
- Group a set of numerical values into a set of **"bins"**
    - i.e "price" is a feature range from 5,000 to 45,000
    - price: 
        - 5000,10000,12000,12000     **bin: Low**
        - 30000,31000     **"bin: Mid**
        - 39000,44000,445000     **bin: High**



**Binning in Python**
|price|
|-----|
|13495|
|16500|
|18920|
|41315|
|5151|
|6295|
|...|

|price|price-binned|
|:---:|:----------:|
|13495|Low|
|16500|Low|
|18920|Medium|
|41315|High|
|5151|Low|
|6295|Low|
|...|...|


- bins = np.linspace(min(df["price"])max(df["price"]),4)
- group_names=["Low","Medium","High"]
- df["price-binned"]= pd.cut(df["price"],bins,labels=group_names,include_lowest=True)

**Visualizing binned data**
- Histograms


# **Turning Categorical Variables into Quantitative Variables in Python**
Problem:
- Most statistacal models cannot take in the objects/strings as input
|Car|Fuel|...|
|---|----|---|
|A|gas|...|
|B|diesel|...|
|C|gas|...|
|D|gas|...|

Solution:
- Add dummy variables for each unique category
- Asign 0 or 1 in each category

|Car|Fuel|...|gas|diesel|
|---|----|---|:-:|:----:|
|A|gas|...|1|0|
|B|diesel|...|0|1|
|C|gas|...|1|0|
|D|gas|...|1|0|

This is oftern referred to as **"One-hot encoding"**


### **Dummy Variables in Python Pandas**
- Use pandas.get_dummies() method
- Convert categorical variables to dummy variables (0 or 1)
- You use indicator variables so you can use categorical variables for regression analysis in the later modules


|Fuel|
|----|
|gas|
|diesel|
|gas|
|gas|

**pd.get_dummies(df['fuel'])** 


|gas|diesel|
|:-:|:----:|
|1|0|
|0|1|
|1|0|
|1|0|

- dummy_variable_1 = pd.get_dummies(df["fuel-type"])
- dummy_variable_1.head()
- Change the names for clarity
    - dummy_variable_1.rename(columns={'gas':'fuel-type-gas', 'diesel':'fuel-type-diesel'}, inplace = True)
- Merge data frame "df" and "dummy_variable_1"
    - df = pd.concat([df, dummy_variable_1], axis = 1
- Drop original column "fuel-type" from "df"
    - df.drop("fuel-type",axis = 1, inplace = True)
    - df.head()


Example:
- In a data set "horsepower" ranges from 48 to 288 with 59 unique values. If you only care which cars have high horsepower, medium horsepower, and little horsepower, you can rearrange them into 3 bins to simplify analysis.
- make sure it is in the correct format
- df['horsepower'] = df['horsepower'].astype(int, copy = True)
    - %matplotlib inline
    - import matplotlib as plt
    - from matplotlib import pyplot
    - plt.pyplot.hist(df["horsepower"])
        - Set x/y labels and plot title
            - plt.pyplot.xlabel("horsepower")
            - plt.pyplot.ylable("count")
            - plt.pyplot.title("horsepower bins")
    - Find 3 bins of equal size bandwidth by using Numpy's **linspace(start_value, end_value, numbers_generated) function**
    - since you want to include the minimum value of horsepower, set start_value = min(df["horsepower"])
    - since you want to include the maximum alue of horsepower, set end_value = max(df["horsepower"])
    - Since you are building 3 bins of equal length, you need 4 dividers, so numbers_generated = 4
        - bins = np.linspace(min(df["horsepower"]), max(df["horsepower"]), 4)
        - bins
    - To set the names of the groups
        - group_names = ["Low","Medium","High"]
    - Apply the function "cut" to determine what each value of df["horsepower"] belongs to
        - df['horsepower-binned'] = pd.cut(df['horsepower']), bins, labels = group_names, include_lowest=True_
        - df[['horsepower','horsepower-binned']].head(20)
    - To see the number of vehicles in each bin:
        - df["horsepower-binned"].value_counts()
    - Plot the distribution of each bin:
        - %matplotlib inline
        - import matplotlib as plt
        - from matplotlib import pyplot
        - pyplot.bar(group_names, df["horsepower-binned"].value_counts())
    - Set x/y labes and plot title
        - plt.pyplot.xlabel("horsepower")
        - plt.pyplot.ylabel("count")
        - plt.pyplot.title("horsepower bins")
        
        
### **Bins Visualization**
- Normally, you use a histogram to visualize the distribution of bins we created
    - %matplotlib inline
    - import matpolotlib as plt
    - from matplotlib import pyplot
        - Draw histogram of attribute "horsepower" with bins = 3
        - plt.pyplot.hist(df["horsepower"], bins = 3)
    - Set x/y labels and plot title
        - plt.pyplot.xlabel("horsepower")
        - plt.pyplot.ylabel("count")
        - plt.pyplot.title("horsepower bins")
            - this shows the binning result of the attribute "horsepower"

Don't forget to save the new CSV
- df.to_csv('_____.csv')
        

