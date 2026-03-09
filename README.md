# Data Cleaning for Misaligned Data

## Overview
In real-world data environments, exports from legacy Warehouse Management Systems (WMS) or Enterprise Resource Planning (ERP) often produce misaligned rows or fragmented records. This project demonstrates a Python-based automated cleaning pipeline that restores structural integrity to broken datasets, ensuring they are ready for downstream analysis or dashboarding.

### Transformation
<p align="center"> <img src="Data Cleaning for Misaligned Data.png" alt="Data Cleaning Transformation" width="800"></p>

## Problem
The raw dataset contained several structural issues that would break standard pivot tables or SQL imports:
* **Shifted Rows**: Key identifiers like **Customer Code** and **Description** were missing in intermittent rows.
* **Injected Headers**: Metadata headers appearing mid-dataset
* **Null Fragementation**: Critical categorical data (Category, Band) was missing in records where the **No** or **Customer Code** was misaligned.

## Solution
A Python script is developed utilizing **Pandas** to programmatically "fix" the dataset. The logic follows these key steps:
1. **Header Identification**: Removing redundant header rows
2. **Isolation**: Splitting the messy DataFrame into 5 distinct feature sets (No, Customer Code and Name, Item Information, Category and Quantity)
3. Noise Filtering: Using **.dropna()** on each subset to remove the 'empty' rows that were causing the misalignment
4. **Index Normalization**: Applying **.reset_index(drop=True)** to each subset
5. **Reconstruction**: Using **pd.concat(axis=1)** to merge the cleaned columns back into a single, structurally DataFrame
6. **Data Type Validaiton**: Ensuring numerical fields like **Qty** are correctly cast

## Business Value
* **Efficiency**: Reduced manual data cleaning time
* **Accuracy**: Eliminate the risk of unattributed records, ensuring every SKUs is correctly mapped to its respective row
* **Scalability**: The script can process thousands of rws of mismatched records in seconds, a task that would hours in Excel
