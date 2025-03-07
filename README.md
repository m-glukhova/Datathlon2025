import pandas as pd
from collections import defaultdict

# Read the Excel file from GitHub
github_url = "https://raw.githubusercontent.com/m-glukhova/Datathlon2025/main/Meteorologia%20structure.xlsx"
df = pd.read_excel(github_url)

# Display first few rows
print(df.head())


