# Pandas Tutorial Essential

This is tutorial repository about pandas.

[Go to Real Cool Heading section](#real-cool-heading)

###Task list

- [x] Information
- [ ] Content


##Contant

1. Add column
2. Add or create new column and add some other column data
3. Rename specific column name
4. Drop column
5. Drop column based on specific
6. split dataframe into multiple dataframe by no of rows

-----------------------


```import pandas as pd```


###1. Add column
```df["new_column"] = ""```


###2. Add or create new column and add some manuplated data from other column

```df["domain_name"] = df["email_id"].apply(lambda x: x.split("@")[-1])```

### Update column data based on other column conditons

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


### Drop records based on column conditons

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

### Split dataframe into mulitple sheet based on record count

```
df_new1, df_new2 = df[:10, :], df[10:, :] if len(df) > 10 else df, None
```


#Real Cool Heading
This is a real cool heading with some real cool content.
