# livestock-analysis<img width="1440" alt="Screenshot 2025-04-15 at 23 03 14" src="https://github.com/user-attachments/assets/c4af4ff5-337c-444b-9303-433a057e65c8" />
<img width="1440" alt="Screenshot 2025-04-15 at 23 04 13" src="https://github.com/user-attachments/assets/f6c5c467-8d07-4266-80d6-2a67e8fa94e0" />
import pandas as pd
import matplotlib.pyplot as plt

# Path to the dataset
file_path = '/Users/anush/Desktop/Т-03-06-Г (2024) рус .xls'

# Load the dataset
df = pd.read_excel(file_path, sheet_name=None)  # Load all sheets

# Get sheet names to understand structure
sheet_names = df.keys()
print("Sheet names:", sheet_names)

# Load a specific sheet, for example, '1.' (update this according to your data sheet structure)
df = df['1.']  # Update sheet name if needed

# Show the first few rows to inspect the data
print("First few rows of the dataset:")
print(df.head())

# Initial inspection of the data
print("\nData Info:")
print(df.info())  # Information on data types, non-null counts, etc.

print("\nDescriptive Statistics:")
print(df.describe())  # Summary statistics

print("\nMissing Values in Columns:")
print(df.isnull().sum())  
df_cleaned = df.dropna()

print("\nCleaned Data (first 5 rows):")
print(df_cleaned.head())

cleaned_file_path = '/Users/anush/Desktop/cleaned_livestock_data.xlsx'
df_cleaned.to_excel(cleaned_file_path, index=False)
print(f"\nCleaned data saved to: {cleaned_file_path}")

# Visualizations

columns = df_cleaned.columns
print("\nColumns in cleaned data:")
print(columns)

if '2024г.' in df_cleaned.columns:
    df_cleaned['2024г.'].dropna().hist(figsize=(10, 6), bins=20)
    plt.title('Distribution of Data for 2024')
    plt.xlabel('Value')
    plt.ylabel('Frequency')
    plt.show()
else:
    print("The column '2024г.' was not found. Please check the column name.")

if 'Unnamed: 0' in df_cleaned.columns:
    df_cleaned['Unnamed: 0'].value_counts().plot(kind='bar', figsize=(10, 6))
    plt.title('Livestock Categories Count')
    plt.xlabel('Category')
    plt.ylabel('Count')
    plt.show()

