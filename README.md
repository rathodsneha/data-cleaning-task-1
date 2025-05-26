# data-cleaning-task-1
import pandas as pd

# Upload the file
from google.colab import files
uploaded = files.upload()

# Load CSV file (after uploading)
df = pd.read_csv("netflix_titles.csv")

# Clean the data
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_')
df = df.drop_duplicates()
df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce')
df['country'] = df['country'].fillna('Unknown')
df['rating'] = df['rating'].fillna('Not Rated')
df['duration'] = df['duration'].fillna('Unknown')
df['director'] = df['director'].fillna('Unknown')
df['cast'] = df['cast'].fillna('Unknown')

# Save to Excel
df.to_excel("netflix_cleaned.xlsx", index=False)

# Download the Excel file
files.download("netflix_cleaned.xlsx")
