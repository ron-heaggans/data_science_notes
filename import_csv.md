# **Importing CSV Data Sets into Jupyter Notebooks**

### **Import Neccessary Modules** 
- Import pandas as pd
- Import numpy as np


### **Accessing CSV as a DataFrame**
- Put file name in object
    - file_name = '______.csv'
- df = pd.read_csv(file_name, header=None)
- df.head(n)


### **Adding Headers to Data Set**
- headers = ["column_1_name", "column_2_name", "column_3_name",...]
- df.columns = headers
- df.columns


### **Cleaning up the Data**
- Replace the "?" symbol with NaN so the dropna() can remove the missing values:
    -  df1=df.replace('?',np.NaN)
- Drop missing values along the column:
    - df=df1.dropna(subset=["column_1_name"],axis=0
        - Here, `axis=0` means that the contents along the entire row will be dropped wherever the entity 'price' is found to be NaN


### **Find the name of the columns**
- print(df.columns)


### **Save the Data Set
- Correspondingly, Pandas enables you to save the data set to CSV. By using the dataframe.to_csv() method, you can add the file path and name along with quotation marks in the brackets.
- For example, if you save the data frame df as automobile.csv to your local machine, you may use the syntax below, where index = False means the row names will not be written.
- df.to_csv("automobile.csv", index=False)


### **Read/Save Other Data Formats**
|Data Format|Read|Save|
|:----------|:--:|:--:|
|csv|pd.read_csv()|df.to_csv()|
|json|pd.read_json()|df.to_json()|
|excel|pd.read_excel()|df.to_excel()|
|hdf|pd.read_hdf()|df.to_hdf()|
|sql|pd.read_sql()|df.to_sql()|


### **Data Types**
- Data has a variety of types.
- The main types stored in Pandas data frames are:
    - object
    - float
    - int
    - bool
    - datetime64
- In order to better learn about each attribute, you should always know the data type of each column.
- In Pandas:
    - df.dtypes

### **Describe**
- To get a statistical summary of each column such as count, column mean value, column standard deviation, etc., use the describe method:
- This method will provide various summary statistics, excluding NaN (Not a Number) values.
    - dataframe.describe()
        - df.describe()
        - df.describe(include = "all")


### **Selecting Columns in the Dataframe**
- dataframe[[' column 1 ',column 2', 'column 3']]
- dataframe[[' column 1 ',column 2', 'column 3']].describe()


### **Info**
- You can also use another method to check your data set:
    - dataframe.info()