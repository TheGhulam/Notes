# Loading Data

### Reading CSVs
> pd.read_csv? # To check parameters associated with the command

```python
df = pd.read_csv('data/btc-market-price.csv')
df.head()
df.ow()

df.columns = ['Timestamp', 'Price'] # If the df doesn't already have columns
pd.to_datetime(df['Timestamp'])
df['Timestamp'] = pd.to_datetime(df['Timestamp'])
df.set_index('Timestamp', inplace=True)

# OR

df = pd.read_csv(
	'data/btc-market-price.csv',
	header=None,
	names=['Timestamp', 'Price'],
	index_col=0,
	parser_dates=[0]
	na_values=['', '?', '-']
	dtype={'Price':'float'}
)


```

### Reading from Relational DataBases

```python
import sqlite3

# Create a connection object
conn = sqlite3.connect('chinook.db')
# Create a Cursor object (allow us to execute sql queries)
cur = conn.cursor()
# Cursor created a method execute, which will receive sql parameters to run against the database
cur.execute('SELECT * FROM employess LIMIT 5;')
# Didn't assign the result of the above query to a variable. This is because we need to run another command to actually fetch the results.
# We can use the fetchall method to fetch all of the results of a query
results = cur.fetchall()
df = pd.DataFrame(results)
# It is good practice to close the connetion and cursor objects that are open. THis prevents the sqlite database from being locked.
cur.close()
conn.close()

# read_sql method
conn = sqlite3.connect('chinook.db')
df = pd.read_sql('SELECT * FROM employees;', conn)
df.head()
df = pd.read_sql('SELECT * FROM employees;', conn, 
				 index_col='EmployeeId',
				 parse_dates=['BirthDate', 'HireDate'])

# read_sql_query method
conn = sqlite3.connect('chinook.db')
df = pd.read_sql_query('SELECT * FROM employees LIMIT 5;', conn)
df.head()
df = pd.read_sql_query('SELECT * FROM employees;', conn,
                       index_col='EmployeeId',
                       parse_dates=['BirthDate', 'HireDate'])

# read_sql_table method
from sqlalchemy import create_engine
engine = create_engine('sqlite:///chinook.db')

connection = engine.connect()
df = pd.read_sql_table('employees', con=connection)
df = pd.read_sql_table('employees', con=connection,
                       index_col='EmployeeId',
                       parse_dates=['BirthDate', 'HireDate'])
connection.close()

# Creatind tables from dataframe objects
cur = conn.cursor()
cur.execute('DROP TABLE IF EXISTS employees2;')
cur.close()
df.to_sql('employees2', conn)
pd.read_sql_query('SELECT * FROM employees2;', conn).head()

```

### Reading from HTML tables
```python
pip install lxml
import pandas as pd	

dfs = pd.read_html(<url> OR <html_string>)
len(dfs) # To check how many tables were parsed

```

### Reading from excel files
```python
df = pd.read_excel('products.xlsx',
				  sheet_name=<sheet_name>,
				  startrow=2
				  startcol=1)

# Can also use ExcelFile class (More Advanced)
# Can also use ExcelWriter object

```

### Loading into Dataframes
Data frames are a number of pandas seried combined into one table with optional indexes


> To check whether an operation is changing the main dataframe, look for the equals operator. If there is an equal sign then the operation is most probably mutable

```python
certificates_earned = pd.DataFrame({
    'Certificates': [8, 2, 5, 6],
    'Time (in months)': [16, 5, 9, 12]
})
names = ['Tom', 'Kris', 'Ahmad', 'Beau']
certificates_earned.index = names

df.head()
df.tail(<optional:3>)
df.info()
df.size()
df.shape()
df.describe()
df.dtypes()
df.dtypes.value_counts()
df.value_counts(normalize=True).	
df.sample(5) # Random sample of 5 rows
```
# Cleaning Data

### Change index
```python
df_population.set_index(['country'], inplace=True)
```

### Check for missing values
> np.nan is a like a virus. Anything it touches, becomes a np.nan

```python
pd.isnull(np.nan) # True
pd.isnull(None) # True
pd.isna(np.nan) # True
pd.isna(None) # True
dogs.isna().any() # Missing value in column
dogs.isna().sum() # Count NaNs in column		.	

pd.notnull(np.nan) # False

s = pd.Series([1, 2, 3, np.nan, np.nan, 4])

s.notnull()
# Returns: 
# 	0 True
# 	1 True
# 	2 True
# 	3 False
# 	4 False
# 	5 True

s[s.notnull()]

s.dropna()
s.dropna(how='any') # Default behaviour
s.dropna(how='all')
s.dropna(thresh=3)
s.dropna(thresh=3, axis='columns')

df['Gender'].unique()
df['Gender'].value_counts()
```

### Filtering missing values
```python
a = np.array([1, 2, 3, np.nan, np.nan, 4])

a[np.isfinite(a)]
# Returns: 
# 	array([1., 2., 3., 4.])
a[np.isfinite(a)].sum()
a[np.isfinite(a)].mean()

apps_with_size_and_rating_present = apps[(~apps['Rating'].isnull()) & (~apps['Size'].isnull())]
```
### Fill in missing values
```python
s.fillna(0)
s.fillna(s.mean())

s.fillna(method='ffill', axis=<optional>)
s.fillna(methos='bfill')

df['Gender'].replace('D', 'F')
df['Gender'].replace('D': 'F', 'N': 'M')
```

### Cleaning Duplicates
```python
ambassadors.duplicated() # Sets element to True when first realizes there are duplicates
ambassadors.duplicated(keep='last') # Keep the last duplicate
ambassadors.duplicated(keep=False) # Identify all duplicates

ambassadors.drop_duplicates()
ambassadors.drop_duplicates(keep='last')
ambassadors.drop_duplicates(keep=False)
vet_visits.drop_duplicated(subset='name')

dframe.duplicated(subset=[<column name>])
dframe.duplicated(subset=[<column name>], keep='last')

```

### Splitting columns
```python
df['Data'].str.split('_')
df['Data'].str.split('_', expand=True)
df['Year'].str.contains('\?')
df['Year'].str.strip()
df['Year'].str.replace(' ', '')
df['Year'].str.replace(r'(?P<year>\d{4}\?', lambda m: m.group('year'))
# 1970? -> 1970
```
### Str -> Number
```python
# List of characters to remove
chars_to_remove = ['+', '$', ',']
# List of column names to clean
cols_to_clean = ['Installs', 'Price']

# Loop for each column
for col in cols_to_clean:
    # Replace each character with an empty string
    for char in chars_to_remove:
        apps[col] = apps[col].astype(str).str.replace(char, '')
    # Convert col to numeric
    apps[col] = pd.to_numeric(apps[col]) 
```
### Cleaning Dates
```python
pulls['date'] = pd.to_datetime(pulls['date'], utc=True)
pulls['date'].dt.month

counts = by_author.groupby(['user', by_author['date'].dt.year]).agg({'pid': 'count'}).reset_index()


```
# Using Data

## Indexing and Slicing
1. Select by index through (Label-based selection):
```python
df.loc['Canada']
df.loc['France': 'Italy']
df.loc['2016': '2018'] # Partial dates are supported


# 2nd dimension
df.loc['France': 'Italy', 'Population']
df.loc['France': 'Italy', ['Population', 'GDP']]
df.loc[:, ['taster_name', 'taster_twitter_handle', 'points']]
df.loc[0, 'contry']

```

2. Select through sequential position (Index Based Selection):
```python
df.iloc[-1]
df.iloc[[0, 1, -1]]
df.iloc[1:3]
df.iloc[1:3, 3]
df.iloc[1:3, [0, 3]]
df.iloc[1:3, 1:3]

# Returns the specified rows
''' 
Both loc and iloc are row-first, column-second.
This is the opposite of what we do in native Python,
which is column-first, row-second.
'''
'''
This means that it's marginally easier to retrieve rows, and marginally harder to get retrieve columns. 
To get a column with iloc, we can do the following:
reviews.iloc[:, 0]
'''
'''
When choosing or transitioning between loc and iloc, there is one "gotcha" worth keeping in mind,
which is that the two methods use slightly different indexing schemes.
iloc uses the Python stdlib indexing scheme, where the first element of the range is included and the last one excluded. 
So 0:10 will select entries 0,...,9. 
loc, meanwhile, indexes inclusively. 
So 0:10 will select entries 0,...,10
'''
```

3. Select Column
```python
df['Population']
# OR
df.Population
```

4. Indexes make subsetting simpler
```python
# Indexes violate 'tidy data' principles
# You need to learn two syntaxes	
dogs[dogs['name'].isin(['Bella', 'Stella'])]
OR
dogs.set_index('name')
dogs.loc[['Bella', 'Stella']]
```

5. Multi-indexing
```python
dogs.set_index(['breed', 'color'])
dogs_loc[[('labrador', 'brown'), ('chihuahua', 'tan')]]
```

6. Sorting index
```python
dogs.sort_index(level=['breed', 'color'], ascending=[True, False])
```
## Conditional selection (boolean arrays)

```python
df['Population'] > 70
# Returns :
#	Canada True
#	Fance False
#	Germany True


df.loc[df['Population'] > 70 ]
# Returns: 
# 	Canada 		30		300		100
# 	Germany 	70		300		422	

df.loc[df['Population'] > 70 , ['Population', 'GDP']]
# Returns:	
# 			Population 	GDP
# 	Canda	80			200	
# 	Germany 100			300
	
'''
"isin"
isin lets you select data whose value "is in" a list of values. 
For example, here's how we can use it to select wines only from Italy or France:
'''
states = ['a', 'b', 'c']
states_df = df[df['states'].isin(states)]

reviews.loc[reviews['country'].isin(['Italy', 'France'])] # Returns: data frame

'''
"isnull" & "notnull"
These methods let you highlight values which are (or are not) empty (NaN). 
For example, to filter out wines lacking a price tag in the dataset, here's what we would do:
'''
reviews.loc[reviews.price.notnull()] # Returns: data frame
```
## Querying Data
```python
stocks.query('nike >= 90')
stocks.query('nike >= 90 and disney < 140')
```
## Applying Functions to Data
### Functions to Series
```python
df_5['A'].map(lambda x: x**2)
top15['Population Estimate'].apply(lambda x: '{0:,}'.format(x)).astype(str)

```
### Functions to DataFrames
```python
df_5 = pd.DataFrame({'A': range(3), 'B': range(1, 4)})
df_5.transform(lambda x: x+1)
df_5.transform(lambda x: x**2)
df_5.transform(lambda x: np.sqrt(x))
# You can transform using multiple functions
df_5.transform([lambda x: x**2, lambda x: x**3])
# Passing a dictionary allows you to perform different calculations
# on different columns
df_5.transform({'A': lambda x: x**2, 'B': lambda x: x**3})

df_5.applymap(lambda x: x**2)
```

## Grouping and Sorting
```python
df = top15.set_index('Continent').groupby(level=0)['Population Estimate'].agg({'size': np.size, 'sum': np.sum, 'mean': np.mean, 'std': np.std})

```
```python
dogs[dogs['color'] == 'Black']['weight'].mean()
dogs[dogs['color'] == 'White']['weight'].mean()
dogs[dogs['color'] == 'Blue']['weight'].mean()
dogs[dogs['color'] == 'Brown']['weight'].mean()
dogs[dogs['color'] == 'Grey']['weight'].mean()

OR

dogs.groupby('color')['weight'].mean()
dogs.groupby(['color', 'breed'])['weight','height'].agg([max, min, mean])

# Count number of repeated rows
counted_df = licenses.groupby('title').agg({'account':'count'}) 

# groupby index keys
df.groupby(level=0).agg()
```


1. Create a Series whose index is the taster_twitter_handle category from the dataset, and whose values count how many reviews each person wrote.
```python
reviews.groupby('taster_twitter_handle').size()
```
2. What is the best wine I can buy for a given amount of money? Create a Series whose index is wine prices and whose values is the maximum number of points a wine costing that much was given in a review. Sort the values by price, ascending (so that 4.0 dollars is at the top and 3300.0 dollars is at the bottom).
```python
best_rating_per_price = reviews.groupby('price')['points'].max().sort_index()
```
3. What are the minimum and maximum prices for each variety of wine? Create a DataFrame whose index is the variety category from the dataset and whose values are the min and max values thereof.
```python
price_extremes =reviews.groupby('variety').price.agg([min, max])
```
4. What are the most expensive wine varieties? Create a variable sorted_varieties containing a copy of the dataframe from the previous question where varieties are sorted in descending order based on minimum price, then on maximum price (to break ties).
```python
sorted_varieties = price_extremes.sort_values(by=['min', 'max'], ascending=False, axis=0)
```
5. Create a Series whose index is reviewers and whose values is the average review score given out by that reviewer. Hint: you will need the taster_name and points columns.
```python
reviewer_mean_ratings = reviews.groupby('taster_name').points.mean()
```

6. What combination of countries and varieties are most common? Create a Series whose index is a MultiIndexof {country, variety} pairs. For example, a pinot noir produced in the US should map to {"US", "Pinot Noir"}. Sort the values in the Series in descending order based on wine count.
```python
country_variety_counts = reviews.groupby(['country', 'variety']).size().sort_values(ascending=False)
```

```python
ans_series.argmax()
ans_series.idmax()
```
### Pivot table
```python
dogs.groupby('color')['weight'].mean()
OR
dogs.pivot_table(values='weight', index='color')
dogs.pivot_table(values='weight', index='color', aggfunc=np.median)

dogs.groupby(['color', 'breed'])['weight'].mean()
OR
dogs.pivot_table(values='weight', index='color', columns='breed', fill_value=0, margin=True)


# Un-Pivot
.melt
'''Arguments
id_vars = []
value_vars = []
var_name = ''
value_name = ''
'''

social_tall = social.melt(id_vars=['financial', 'company'], value_vars=['2018', '2017'], var_name=['year'], value_name='dollars')
```

## Dropping Stuff
> Opposed to the concept of selection, we have "dropping". Instead of pointing out which values you'd like to select you could print which ones you'd like to drop:

```python
df.drop('Canada')
df.drop(colums=['Population', 'HDI'])
df.drop(['Italy', 'Canada'], axis=0)
df.drop(['Population', 'HDI'], axis=1)
df.drop(['Population', 'HDI'], axis='colums')
```
## Creating columns from columns
```python
df[['Population', 'GDP']]
df['GDP'] / df['Population']
df['GDP Per Capita'] = df['GDP'] / df['Population']
```


## Merging DataFrames
```python
''' Types of Joins:
inner, outer, left, right
semi-join, anti-join (Returns left table, excluding intersection; Only returns columns from left table)
'''

pd.merge(df_1, df_2, how='inner', left_index=True, right_index=True)
pd.merge(df_1, df_2, how='outer', left_index=True, right_on=<Column Name>)
pd.merge(df_1, df_2, how='left', left_on=<Column Name>, right_on=<Column Name>)
wards_census = wards.merge(census, on='ward', suffixes=('_cen', '_ward'))
'''Arguments
on=
left_on=
right_on=
validate='one-to-one'
verify_integrity=True
'''

pd.merge_ordered()
'''Arguments
fill_method='ffill'
'''
pd.merge_asof()
'''Arguments
direction='forward'
'''
# Merged 'on' columns must be sorted

# Connect tables vertically
pd.concat([table1, table2, table2])
''' Arguments
axis=0
join='inner'
sort=True
ignore_index=False
keys = []
'''
df = pd.concat([df1['country'], df2['country']]).unique()

pd.append()
''' Arguments
ignore_index=True
sort=True
'''
```
## Statistics
```python
ics_df.count()
ics_df.sum(skipna=True)
ics_df["Sales"].mean()
ics_df["Sales"].median()
ics_df["Sales"].mode()
ics_df["Sales"].min()
ics_df["Sales"].max()
ics_df["Sales"].prod() # Product of values
ics_df["Sales"].std() # Standard deviation
ics_df["Sales"].var() # Variance
ics_df["Sales"].sem() # Standard error
ics_df["Sales"].skew()
ics_df["Sales"].kurt()
ics_df["Sales"].quantile(.5)
ics_df["Sales"].cumsum()
ics_df["Sales"].cumprod()
ics_df["Sales"].cummax()
ics_df["Sales"].cummin()
ics_df.describe()

# .agg
'''
The .agg() method allows you to apply your own custom functions to a DataFrame, 
as well as apply functions to more than one column of a DataFrame at once, making your aggregations super efficient.
'''
df_2.agg(np.mean)
df_2.agg(['mean', 'std'])

def pct30(column):
	return column.quantile(0.3)
df_2['weight'].agg(pct30)

def pct40(column):
	return column.quantile(0.4)
df_2[['height','wehight']].agg([pct30, pct40])
```

## Iteration
```python
# Iterating over series
ser_7 = pd.Series(range(5), index=['a', 'b', 'c', 'd', 'e'])
for col in ser_7:
    print(col)
    
print()
# Iterating over DFs
arr_4 = np.random.randint(10, 50, size=(2, 3))
df_8 = pd.DataFrame(arr_4, ['B', 'C'], ['C', 'D', 'E'])
print(df_8)

# items allows you to iterate through key value pairs to make
# calculations 1 column at a time
for label, ser in df_8.items():
    print(label)
    print(ser)
    
print()


## Un-efficient since creating new series every time use apply instead
# You can also iterate through rows
for index, row in df_8.iterrows():
    print(f"{index}\n{row}")
print()

# Get a tuple that contains row data
for row in df_8.itertuples():
    print(row)
```

## Bins
```python
df['Renewable'] = pd.cut(df['Renewable'], 5)
```
## Classification
```python
df['> median'] = np.where(df['% Renewable'] >= np.median(top15['% Renewable']), 1, 0)
```

# Visualizations
## Matplotlib - Global API
```python
# Eg. 1
x = np.arange(-10, 11)
plt.figure(figzie=(12, 6))
plt.title('My Nice Plot')
plt.plot(x, x ** 2)
plt.plot(x, -1 * (x ** 2))

# Eg.2
plt.figure(figsize=(12, 6))
plt.title('My Nice Plot')

plt.subplot(1, 2, 1)  # rows, columns, panel selected
plt.plot(x, x ** 2)
plt.plot([0, 0, 0], [-10, 0, 100])
plt.legend(['X^2', 'Vertical Line'])
plt.xlabel('X')
plt.ylabel('X Squared')

plt.subplot(1, 2, 2)
plt.plot(x, -1 * (x ** 2))
plt.plot([-10, 0, 10], [-50, -50, -50])
plt.legend(['-X^2', 'Horizontal Line'])

plt.xlabel('X')
plt.ylabel('X Squared')


# Example
import matplotlib.pyplot as plt
import numpy as np

plt.figure()

languages =['Python', 'SQL', 'Java', 'C++', 'JavaScript']
pos = np.arange(len(languages))
popularity = [56, 39, 34, 34, 29]

# change the bar colors to be less bright blue
bars = plt.bar(pos, popularity, align='center', linewidth=0, color='lightslategrey')
# make one bar, the python bar, a contrasting color
bars[0].set_color('#1F77B4')

# soften all labels by turning grey
plt.xticks(pos, languages, alpha=0.8)
plt.ylabel('% Popularity', alpha=0.8)
plt.title('Top 5 Languages for Math & Data \nby % popularity on Stack Overflow', alpha=0.8)

# remove all the ticks (both axes), and tick labels on the Y axis
plt.tick_params(top='off', bottom='off', left='off', right='off', labelleft='off', labelbottom='on')

# remove the frame of the chart
for spine in plt.gca().spines.values():
    spine.set_visible(False)
plt.show()

# You don't know what plot you are referring to

# Histogram
plt.hist(bins=10, alpha=0.8)


# Scatter plots
dogs.plot(..., kind='scatter')
```
### Seaborn
```python
sns.set_style('white')

iris = pd.read_csv('iris.csv')
iris.head()
sns.pairplot(iris, hue='Name', diag_kind='kde', size=2);
plt.figure(figsize=(8,6))
plt.subplot(121)
sns.swarmplot('Name', 'PetalLength', data=iris);
plt.subplot(122)
sns.violinplot('Name', 'PetalLength', data=iris);


# Jointplots
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib notebook

plt.figure()
sns.jointplot(v1, v2, alpha=0.2);

grid = sns.jointplot(v1, v2, alpha=0.4);
grid.ax_joint.set_aspect('equal')

# Hexbin plots
sns.jointplot(v1, v2, kind='hex');
```

## Matplotlib - OOP Interface
```python
fig, axes = plt.subplots(figsize=(12, 6))

axes.plot(seattle_weather['MONTH'],
		 seattle_weather['MLY-PRCP-NORMAL'],
		 marker='v',
		 linestyle='--',
		 color='r',
		 yerr=seattle_weather['MLY-TAVG-STDEV'])

axes.set_xlabel('X')
axes.set_ylabel('X Squared')
axes.set_title("My Nice Plot")

plt.show()


fig, ax = plt.subplots(3, 2, sharey=True)
ax.shape = (3,2)
ax[0, 0].plot(seattle_weather['MONTH'],
		 seattle_weather['MLY-PRCP-NORMAL'],
		 marker='v',
		 linestyle='--',
		 color='r')

# Using twin axes
fig, ax = plt.subplots()
ax.plot(climate_change.index, climate_change["co2"], color='blue')
ax.set_xlabel('Time')
ax.set_ylabel('CO2 (ppm)', color='blue')
ax.tick_params('y', colors='blue')

ax2 = ax.twinx()
ax2.plot(climate_change.index,          climate_change["relative_temp"],          color='red')
ax2.set_ylabel('Relative temperature (Celsius)', color='red')
ax2.tick_params('y', colors='red')
plt.show()

# Annotation
ax2.annotate('>1 degree', 
			 xy=(pd.Timestamp('2015-10-06'), 1),
			 xytext=(pd.Timestamp('2008-10-06', -0.2),
			 arrowprops={"arrowstyle":'->',color=''})

```
### Bar charts
```python
# Stacked bar charts
# Add bars for "Gold" with the label "Gold"
ax.bar(medals.index, medals['Gold'], label='Gold')

# Stack bars for "Silver" on top with label "Silver"
ax.bar(medals.index, medals['Silver'], bottom=medals['Gold'], label='Silver')

# Stack bars for "Bronze" on top of that with label "Bronze"
ax.bar(medals.index, medals['Bronze'], bottom=medals['Gold'] + medals['Silver'], label='Bronze')

'''Arguments
yerr=
'''
# Display the legend
ax.legend()

plt.show()
```
### Histograms 
```python
fig, ax = plt.subplots()

# Plot a histogram of "Weight" for mens_rowing
ax.hist(mens_rowing['Weight'], label='Rowing', histtype='step', bins=5)

# Compare to histogram of "Weight" for mens_gymnastics
ax.hist(mens_gymnastics['Weight'], label='Gymnastics', histtype='step', bins=5)

ax.set_xlabel("Weight (kg)")
ax.set_ylabel("# of observations")

# Add the legend and show the Figure
ax.legend()
plt.show()
'''arguments
bins = 10 
OR
bins = [10, 20, 30]
histtype = 'step'
'''
```

### Box plots
```python
fig, ax = plt.subplots()
ax.boxplot([mens_rowing['Height'],
			mens_gymnastics['Height']])
ax.set_xticklabels(['Rowing', 'Gymnastics'])
ax.set_ylabel('Height (cm)')
```

### Scatter plots
```python
fig, ax = plt.subplots()
ax.scatter(climate['co2'], climate['relative_temp'])
ax.set_xlabel('CO2 (ppm)')
ax.set_ylabel('Relative temp (Celsius)')
plt.show()

'''Arguments
c=climate.index
'''
```

### Styles
```python
plt.style.use("seaborn-colorblind")
fig, ax = plt.subplots()
...
```

### Sharing your visualizations
```python
fig, ax = plt.subplots()
...

fig.set_size_inches([5, 3]) #[width, height]

fig.savefig("gold_medals.png", dpi=300)
fig.savefig("gold_medals.jpg", quality=50)
fig.savefig("gold_medals.svg")
```
Automating figures from data  
Why automate?
- Ease and speed
- Flexibility
- Robustness
- Reproducibility
```python
sports = ['cricket', 'footabll', 'swimming']

for sport in sports
```
## Seaborn
```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.set_sytle('')

sns.scatterplot(x=<list>, y=<list>)
plt.show()
```
### Customization
```python
sns.set_style('')

sns.set_palette('' OR [])

sns.set_context('paper') # Changing scale
'paper', 'notebook', 'talk', 'poster'


```

### Using pandas with seaborn
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df = pd.read_csv("masculinity.csv")
sns.countplot(x="how_masculine", data=df)
plt.show()
```
### Scatter plots
```python
# scatterplot()
import matplotlib.pyplot as plt
import seaborn as sns
hue_colors = {'yes':'black', 'no':'red'}
sns.scatterplot(x='total_bill',
				y='tip',
				data=tips,
				hue='smoker',
				hue_order=['Yes', 'No'],
			    palette=hue_colors)
```

### Relational plots
```python
# relplot()
sns.relplot(x='total_bill',
			y='tip',
			data=tips,
			kind='scatter',
			col='smoker',
			row='time',
		    col_wrap=2,            
			col_order=["Thur","Fri","Sat","Sun"],
		   	size='size',
		   	hue='size',
		   	style='smoker',
		   	alpha=0.7)

plt.show()

```
### Line plots
```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x='hour'
			y='mean',
			data=co2,
			kind='line',
			syle='location',
			hue='location',
		   	marker=True,
		   	dashes=False,
		   	ci='sd')
```

### Categorical plots
```python
# Bar plot
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(kind='bar')

# Point plot
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(kind='point',
			join=False,
			estimator=median,
			capsize=0.2,
		   	ci=None)

# Box plot
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(kind='box',
			order= <list>,
			sym="" # ommit outliers
			whis=2.0 OR [5, 95](Percentile) # Whiskers
```
## Plotly
```python
import plotly
plotly.offline.init_notebook_mode(connected=True)
import plotly.graph_objs as go

# Print the total number of unique categories
num_categories = len(apps['Category'].unique())
print('Number of categories = ', num_categories)

# Count the number of apps in each 'Category' and sort them in descending order
num_apps_in_category = apps['Category'].value_counts().sort_values(ascending = False)

data = [go.Bar(
        x = num_apps_in_category.index, # index = category name
        y = num_apps_in_category.values, # value = count
)]

plotly.offline.iplot(data)


# Average rating of apps
avg_app_rating = apps['Rating'].mean()
print('Average app rating = ', avg_app_rating)

# Distribution of apps according to their ratings
data = [go.Histogram(
        x = apps['Rating']
)]

# Vertical dashed line to indicate the average app rating
layout = {'shapes': [{
              'type' :'line',
              'x0': avg_app_rating,
              'y0': 0,
              'x1': avg_app_rating,
              'y1': 1000,
              'line': { 'dash': 'dashdot'}
          }]
          }

plotly.offline.iplot({'data': data, 'layout': layout})
```

