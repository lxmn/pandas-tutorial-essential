# Pandas Tutorial Essential

This is tutorial repository about pandas.

[Go to Real Cool Heading section](#real-cool-heading)

### Task list

- [x] Information
- [ ] Content


## Content

1. [Add column](#add-column)
2. [Add or create new column and add some other column data](#add-or-create-new-column-and-add-some-manuplated-data-from-other-column)
3. [Update column data based on other column conditions](#update-column-data-based-on-other-column-conditons)
3. [Rename specific column name](#rename-specific-column-name)
4. [Drop column](#drop-column)
5. [Drop column based on specific condition](#drop-records-based-on-column-conditons)
6. [Group by partial values in column](#group-by-partial-values-in-column)
6. [Split dataframe into multiple dataframe by no of rows](#split-dataframe-into-multiple-dataframe-by-no-of-rows)
7. [Check if string is in a pandas dataframe](#Check if string is in a pandas dataframe)
8. [Strip / trim all strings of a dataframe](#Strip / trim all strings of a dataframe)
9. [How to replace substring in all dataframe by using regex](#How to replace substring in all dataframe by using regex)
10. [How To Convert Two Columns from Pandas Dataframe to a Dictionary](#https://cmdlinetips.com/2021/04/convert-two-column-values-from-pandas-dataframe-to-a-dictionary)
11. [Replace column values based on another dataframe](#11-replace-column-values-based-on-another-dataframe)

-----------------------


```import pandas as pd```


### Create a sample dataframe

```
left = pd.DataFrame(
    {
        "key": ["K0", "K1", "K2", "K3"],
        "A": ["A0", "A1", "A2", "A3"],
        "B": ["B0", "B1", "B2", "B3"],
    }
)
right = pd.DataFrame(
    {
        "key": ["K0", "K1", "K2", "K3"],
        "C": ["C0", "C1", "C2", "C3"],
        "D": ["D0", "D1", "D2", "D3"],
    }
)
result = pd.merge(left, right, on="key")
```

### Add column
```df["new_column"] = ""```


### Add or create new column and add some manipulated data from other column

```df["domain_name"] = df["email_id"].apply(lambda x: x.split("@")[-1])```

### Update column data based on other column conditions

```
import pandas
df = pandas.read_csv("test.csv")
df.loc[df.ID == 103, 'FirstName'] = "Matt"
df.loc[df.ID == 103, 'LastName'] = "Jones"

or

df.loc[df.ID == 103, ['FirstName', 'LastName']] = 'Matt', 'Jones'
```


### Rename specific column name
[Link to stack overflow!](https://stackoverflow.com/a/11354850/3532385)

Use the df.rename() function and refer the columns to be renamed. Not all the columns have to be renamed:
```
df = df.rename(columns={'oldName1': 'newName1', 'oldName2': 'newName2'})
# Or rename the existing DataFrame (rather than creating a copy) 
df.rename(columns={'oldName1': 'newName1', 'oldName2': 'newName2'}, inplace=True)
```


### Drop column
```del df["column_name"]```


### Drop records based on column conditions

```
df = pd.DataFrame({"col_1": (0.0, 0.0, 1.0, 1.0, 0.0, 1.0, 1.0),
    "col_2": (0.0, 0.24, 1.0, 0.0, 0.22, 3.11, 0.0),
    "col_3": ("Mon", "Tue", "Thu", "Fri", "Mon", "Tue", "Thu")})

df_new = df.drop(df[(df['col_1'] == 1.0) & (df['col_2'] == 0.0)].index)
print(df_new)
```

or 

```df = df[~df['Species'].isin(['Cat'])]```



### Short data based on specific column


### Save dataframe in multiple sheet of excel
[link to stack overflow](https://stackoverflow.com/a/58652904/3532385)

```
pip install xlsxwriter

df1 = pd.DataFrame({'website': ['www.dailynews.com', 'www.dailynews.co.zw']})
df2 = pd.DataFrame({'website': ['www.gulf-daily-news.com', 'www.dailynews.gov.bw']})

# Create a new excel workbook
writer = pd.ExcelWriter('title.xlsx', engine='xlsxwriter')

# Write each dataframe to a different worksheet.
df1.to_excel(writer, sheet_name='Sheet1')
df2.to_excel(writer, sheet_name='Sheet2')
writer.save()
```

### Group by partial values in column
```
df = df.groupby(df.Name.str[0:8])

```

### Split dataframe into multiple dataframe based on rows count
```
df_new1, df_new2 = df[:10, :], df[10:, :] if len(df) > 10 else df, None
```

### Check if string is in a pandas dataframe

```
mel_count=a['Names'].str.contains('Mel').sum()
if mel_count>0:
    print ("There are {m} Mels".format(m=mel_count))

Or any(), if you don't care how many records match your query

if a['Names'].str.contains('Mel').any():
    print ("Mel is there")
```

### Strip / trim all strings of a dataframe

```
You can use DataFrame.select_dtypes to select string columns and then apply function str.strip.

Notice: Values cannot be types like dicts or lists, because their dtypes is object.

df_obj = df.select_dtypes(['object'])
print (df_obj)
0    a  
1    c  

df[df_obj.columns] = df_obj.apply(lambda x: x.str.strip())
print (df)

   0   1
0  a  10
1  c   5
```


### How to replace substring in all dataframe by using regex

```
# Cleaning logic by using regualar expression  

df = df.replace(to_replace=r'-1', value='', regex=True)
df = df.replace(to_replace=r'^-', value='', regex=True)
df = df.replace(to_replace=r'#\w+\s*', value='', regex=True)

```

### 10. How To Convert Two Columns from Pandas Dataframe to a Dictionary  (https://cmdlinetips.com/2021/04/convert-two-column-values-from-pandas-dataframe-to-a-dictionary)

```
1st  Method 
dict(zip(df.state, df.name))

2nd Method
pd.Series(df.name.values,index=df.state).to_dict()

```

### 11. Replace column values based on another dataframe (https://stackoverflow.com/questions/24768657/replace-column-values-based-on-another-dataframe-python-pandas-better-way)

```
df1 = pd.DataFrame([["X",1,1,0],
              ["Y",2,2,2],
              ["Z",3,3,3],
              ["Y",4,4,4]],columns=["Name","Nonprofit","Business", "Education"])    
df2 = pd.DataFrame([["Y",11,11],
              ["Z",12,12],
              ['U',13,13]],columns=["Name","Nonprofit", "Education"])
```

```
Way 1:

df1 = df1.merge(df2,on='Name',how="left")
df1['Nonprofit_y'] = df1['Nonprofit_y'].fillna(df1['Nonprofit_x'])
df1['Business_y'] = df1['Business_y'].fillna(df1['Business_x'])
df1.drop(["Business_x","Nonprofit_x"],inplace=True,axis=1)
df1.rename(columns={'Business_y':'Business','Nonprofit_y':'Nonprofit'},inplace=True)

Way 2:

df1 = df1.set_index('Name')
df2 = df2.set_index('Name')
df1.update(df2)
df1.reset_index(inplace=True)
```



# Real Cool Heading

This is a real cool heading with some real cool content.
