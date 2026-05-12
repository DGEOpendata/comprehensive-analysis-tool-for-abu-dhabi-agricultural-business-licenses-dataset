markdown
# Comprehensive Analysis Tool for Abu Dhabi Agricultural Business Licenses Dataset

This repository provides tools and scripts to analyze and visualize the "Agricultural Business Licenses Dataset." The tool enables users to gain insights into the state of the agriculture and livestock sectors in Abu Dhabi. Users can perform analyses on license classification, legal forms, issuance dates, and geospatial distributions.

## Features
- **Data Cleaning**: Automatically clean and preprocess the dataset for analysis.
- **Trend Analysis**: Analyze trends in license issuance over time.
- **Geospatial Visualization**: Map the geographic distribution of licenses (requires shapefile of Abu Dhabi regions).
- **Multi-Format Support**: Supports CSV, JSON, and Excel data formats.
- **Educational Resources**: Includes tutorials and examples to help users navigate the tool.

## Prerequisites
- Python 3.7 or higher
- Required Python libraries:
  - pandas
  - matplotlib
  - geopandas (optional for geospatial analysis)

## Installation
1. Clone this repository:
   bash
   git clone https://github.com/your-repo/agricultural-license-analysis.git
   cd agricultural-license-analysis
   
2. Install the required Python libraries:
   bash
   pip install pandas matplotlib geopandas
   

## Usage
1. Place the dataset (`DL11-Agriculture_and_Fish_and_Animal_Wealth-Licenses-ADRA-OD-015-LAG.xlsx`) in the root directory.
2. Run the script:
   bash
   python analysis_tool.py
   
3. Follow the on-screen instructions to perform analysis and generate visualizations.

## Example Data Analysis
Here's an example of how to analyze the number of licenses issued per year:

python
import pandas as pd
import matplotlib.pyplot as plt

# Load the dataset
data_path = 'DL11-Agriculture_and_Fish_and_Animal_Wealth-Licenses-ADRA-OD-015-LAG.xlsx'
df = pd.read_excel(data_path)

# Data Cleaning
def clean_data(df):
    df = df.rename(columns={
        'License Number': 'license_number',
        'Unified License Number': 'unified_license_number',
        'Trade Name (English)': 'trade_name_en',
        'Trade Name (Arabic)': 'trade_name_ar',
        'Legal Form': 'legal_form',
        'License Type': 'license_type',
        'License Classification': 'license_classification',
        'Establishment Date': 'establishment_date',
        'Issuance Date': 'issuance_date',
        'Expiry Date': 'expiry_date'
    })
    df['issuance_date'] = pd.to_datetime(df['issuance_date'], errors='coerce')
    df['expiry_date'] = pd.to_datetime(df['expiry_date'], errors='coerce')
    return df

df = clean_data(df)

# Example Analysis: Number of licenses issued per year
df['issuance_year'] = df['issuance_date'].dt.year
licenses_per_year = df['issuance_year'].value_counts().sort_index()

# Plot the result
plt.figure(figsize=(10, 5))
licenses_per_year.plot(kind='bar', color='skyblue')
plt.title('Number of Licenses Issued Per Year')
plt.xlabel('Year')
plt.ylabel('Number of Licenses')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()


## Contribution
We welcome contributions from the community to enhance this tool. Please submit a pull request or open an issue for any suggestions or bug fixes.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
