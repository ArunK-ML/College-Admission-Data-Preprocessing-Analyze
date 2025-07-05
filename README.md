# College-Admission-Data-Preprocessing-Analyze
Study different types of data
📥 Step 1: Import Required Library
python
Copy
Edit
import pandas as pd
We use Pandas, a powerful Python library for data analysis and manipulation.

📂 Step 2: Load the Dataset
python
Copy
Edit
df = pd.read_csv('/content/College_Admission_data.csv')
df
We read the CSV file into a DataFrame called df.

🕳️ Step 3: Detecting Missing Values
Check for missing values
python
Copy
Edit
df.isnull()
Returns True where the data is missing (NaN).

Count missing values per column
python
Copy
Edit
df.isnull().sum()
Gives a column-wise count of missing values.

Count non-null values per column
python
Copy
Edit
df.notnull().sum()
Gives a count of non-missing values in each column.

🧪 Step 4: Filling Missing Values
Fill with constant value
python
Copy
Edit
df.fillna(100)
Replaces all NaN values with 100 (temporary – doesn’t update the original DataFrame).

Fill using other rows
Backward Fill (next valid value)
python
Copy
Edit
df.fillna(method='bfill')
Forward Fill (previous valid value)
python
Copy
Edit
df.fillna(method='ffill')
Newer style forward fill
python
Copy
Edit
df.ffill()
Fill a specific column
Backward fill on only hsc column
python
Copy
Edit
df['hsc'] = df['hsc'].bfill()
⚠️ Warning: Using method is deprecated in future Pandas versions.

Fill SSLC column with its mean value
python
Copy
Edit
df['SSLC'] = df['SSLC'].mean()
⚠️ Avoid using inplace=True on chained assignments to prevent unexpected results.

🧹 Step 5: Dropping Missing Values
Drop all rows with any null value
python
Copy
Edit
df.dropna()
Drop all columns with any null value
python
Copy
Edit
df.dropna(axis=1)
⚠️ Be careful — this might delete useful columns.

Drop rows where any of specified columns are null
python
Copy
Edit
df.dropna(how='any', subset=['hsc', 'SSLC', 'arrears'])
Drop rows where all of specified columns are null
python
Copy
Edit
df.dropna(how='all', subset=['hsc', 'SSLC', 'arrears'])

🧬 Step 6: Handling Duplicate Data
Fill NaNs before checking duplicates
python
Copy
Edit
df1 = df.bfill()
Detecting Duplicates
Detect duplicate rows (excluding first)
python
Copy
Edit
df1.duplicated()
Keep first or last duplicate
python
Copy
Edit
df1.duplicated(keep='first')
df1.duplicated(keep='last')
Mark all duplicate rows
python
Copy
Edit
df1.duplicated(keep=False)
Removing Duplicates
Drop duplicates, keep first occurrence
python
Copy
Edit
df1.drop_duplicates(keep='first')
Drop duplicates, keep last occurrence
python
Copy
Edit
df1.drop_duplicates(keep='last')
Drop all duplicates completely
python
Copy
Edit
df1.drop_duplicates(keep=False)
Drop duplicates based on specific columns
Keep last entry for each (sl No, name)
python
Copy
Edit
df1.drop_duplicates(subset=['sl No', 'name'], keep='last')
Remove all duplicate college values
python
Copy
Edit
df1.drop_duplicates(keep=False, subset=['college'])


✅ Summary
Operation	Description
isnull() / notnull()	Detect missing values
fillna() / bfill()	Fill missing values
dropna()	Remove rows/columns with missing data
duplicated()	Identify duplicate rows
drop_duplicates()	Remove duplicate rows
