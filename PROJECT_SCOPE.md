# CSV Data Analyzer - Project Scope

## 📊 Project Overview
This project is an **Employee/HR Data Analyzer** built using Python, NumPy, and Pandas. It demonstrates data analysis skills by reading, processing, analyzing, and visualizing employee data from a CSV file.

## 🎯 Project Objectives
1. Demonstrate proficiency in **NumPy** and **Pandas** libraries
2. Perform exploratory data analysis (EDA) on employee data
3. Extract meaningful insights from HR data
4. Create visualizations to support data-driven decisions
5. Showcase clean, readable, and well-documented code

## 📁 Dataset Description
**File:** `employee_data.csv`

**Columns:**
- `EmployeeID`: Unique identifier for each employee
- `Name`: Employee name
- `Department`: Department (Engineering, Marketing, Sales, HR, Finance)
- `Position`: Job title/role
- `Salary`: Annual salary in USD
- `Age`: Employee age
- `YearsOfExperience`: Total years of professional experience
- `PerformanceRating`: Performance score (1.0 - 5.0)
- `Location`: Office location (Bangalore, Mumbai, Delhi, Hyderabad, Pune)
- `JoinDate`: Date of joining the company

**Dataset Size:** 50 employees

## 🔍 Analysis Tasks to Perform

### 1. Data Loading & Inspection
- Load the CSV file using Pandas
- Display first/last few rows
- Check data types and info
- Identify missing values
- Check for duplicate records

### 2. Statistical Analysis
Compute and display:
- **Descriptive statistics** (mean, median, mode, std deviation)
- **Salary statistics** by department
- **Age distribution** across the organization
- **Experience vs Performance** correlation
- **Department-wise employee count**

### 3. Data Filtering & Querying
Implement filters to:
- Find employees with salary > 80,000
- Filter by specific department(s)
- Get employees with performance rating >= 4.5
- Find employees by location
- Filter by years of experience range
- Employees who joined in a specific year

### 4. Advanced Analysis
- **Top performers:** Employees with highest performance ratings
- **Salary insights:** Highest/lowest paid employees by department
- **Experience analysis:** Average experience by department
- **Tenure analysis:** Calculate years in company from JoinDate
- **Age groups:** Categorize employees into age brackets

### 5. Data Visualization
Create the following visualizations:
- **Bar chart:** Average salary by department
- **Histogram:** Age distribution
- **Scatter plot:** Experience vs Salary
- **Pie chart:** Employee distribution by department
- **Box plot:** Salary distribution across departments
- **Heatmap:** Correlation matrix of numerical columns

### 6. Data Export
- Save filtered/analyzed data to new CSV files
- Export summary statistics to a separate file

## 🛠️ Technical Requirements

### Libraries to Use:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime
```

### Key Functions/Methods to Implement:
1. `load_data()` - Load CSV file
2. `data_overview()` - Display basic info and statistics
3. `filter_data()` - Apply various filters
4. `analyze_salary()` - Salary analysis
5. `analyze_performance()` - Performance metrics
6. `visualize_data()` - Create charts
7. `export_results()` - Save processed data

## 📈 Expected Outputs

### Console Outputs:
- Data summary and statistics
- Filtered results based on user queries
- Top/bottom performers
- Department-wise insights

### Visual Outputs:
- 5-6 different types of charts saved as PNG files
- Clean, labeled, and professional-looking visualizations

### File Outputs:
- Filtered datasets (CSV)
- Summary statistics (CSV/TXT)

## 🎓 Learning Outcomes
By completing this project, you will demonstrate:
1. **Pandas Skills:** Reading CSV, DataFrame operations, filtering, grouping
2. **NumPy Skills:** Array operations, statistical calculations
3. **Data Cleaning:** Handling missing values, data type conversions
4. **Data Analysis:** Descriptive statistics, correlation analysis
5. **Data Visualization:** Creating meaningful charts with Matplotlib/Seaborn
6. **Code Organization:** Writing modular, reusable functions
7. **Documentation:** Writing clear docstrings and comments

## 🚀 Bonus Features (Optional)
- Interactive menu for user to choose analysis options
- Command-line arguments for different operations
- Exception handling for robust code
- Unit tests for key functions
- Data validation and quality checks
- Export analysis report as PDF

## 📝 Deliverables
1. ✅ `employee_data.csv` - Sample dataset
2. ✅ `csv_analyzer.py` - Main Python script
3. ✅ `README.md` - Project documentation
4. ✅ `requirements.txt` - Dependencies list
5. ✅ Charts/visualizations (PNG files)
6. ✅ Sample output files

## 🎯 Success Criteria
- Code runs without errors
- All analysis tasks completed
- Visualizations are clear and insightful
- Code is well-commented and readable
- README provides clear instructions
- Project is ready for GitHub upload

---

**Note:** This project is designed for intermediate-level data analysis positions and demonstrates practical skills that employers look for in data analyst roles.
