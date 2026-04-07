# 📊 CSV Data Analyzer - Employee/HR Analytics

A comprehensive Python-based data analysis project that demonstrates proficiency in **Pandas**, **NumPy**, and **Data Visualization** through real-world HR analytics.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-green.svg)
![NumPy](https://img.shields.io/badge/NumPy-1.24+-orange.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## 🎯 Project Overview

This project analyzes employee data from a company with 50 employees across 5 departments (Engineering, Marketing, Sales, HR, Finance). It demonstrates:

- **Data Loading & Cleaning:** Reading CSV files, handling dates, creating derived features
- **Statistical Analysis:** Computing comprehensive statistics and correlations
- **Data Filtering:** Implementing multiple filter functions for different criteria
- **Advanced Analytics:** Correlation analysis, performance evaluation, tenure calculations
- **Data Visualization:** Creating 6 different types of professional charts
- **Data Export:** Saving filtered results and summary reports

## 📁 Project Structure

```
csv-data-analyzer/
│
├── employee_data.csv           # Sample HR dataset (50 employees)
├── csv_analyzer.py             # Main Python script with all analysis functions
├── README.md                   # Project documentation (this file)
├── PROJECT_SCOPE.md            # Detailed project objectives and tasks
├── STEP_BY_STEP_GUIDE.md       # Complete implementation guide
├── INTERVIEW_QA.md             # Interview questions & answers
├── requirements.txt            # Python dependencies
│
└── outputs/                    # Generated files (created after running)
    ├── salary_by_department.png
    ├── age_distribution.png
    ├── experience_vs_salary.png
    ├── department_distribution.png
    ├── salary_boxplot.png
    ├── correlation_heatmap.png
    ├── high_earners.csv
    └── summary_statistics.txt
```

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- pip (Python package installer)

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/yourusername/csv-data-analyzer.git
cd csv-data-analyzer
```

2. **Create virtual environment (optional but recommended):**
```bash
python -m venv venv

# Activate on Windows:
venv\Scripts\activate

# Activate on Mac/Linux:
source venv/bin/activate
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

### Running the Analysis

Simply run the main script:

```bash
python csv_analyzer.py
```

This will:
- Load the employee data
- Display comprehensive statistics
- Perform correlation analysis
- Create 6 visualizations (saved as PNG files)
- Export filtered data and summary statistics

## 📊 Dataset Description

### employee_data.csv

| Column | Description | Type |
|--------|-------------|------|
| EmployeeID | Unique identifier | String |
| Name | Employee name | String |
| Department | Department name | Categorical |
| Position | Job title | String |
| Salary | Annual salary (USD) | Integer |
| Age | Employee age | Integer |
| YearsOfExperience | Total work experience | Integer |
| PerformanceRating | Performance score (1-5) | Float |
| Location | Office location | Categorical |
| JoinDate | Date of joining | Date |

**Departments:** Engineering, Marketing, Sales, HR, Finance
**Locations:** Bangalore, Mumbai, Delhi, Hyderabad, Pune
**Sample Size:** 50 employees

## 🔍 Key Features

### 1. Data Loading & Inspection
```python
df = load_data('employee_data.csv')
data_overview(df)
```
- Displays first/last rows
- Shows data types and info
- Identifies missing values
- Checks for duplicates

### 2. Statistical Analysis
```python
statistical_analysis(df)
department_analysis(df)
```
- Salary statistics (mean, median, std, min, max)
- Age distribution
- Experience metrics
- Performance ratings
- Department-wise breakdowns

### 3. Data Filtering
```python
high_earners = filter_by_salary(df, min_salary=80000)
eng_dept = filter_by_department(df, 'Engineering')
top_rated = filter_by_performance(df, min_rating=4.5)
```
- Filter by salary range
- Filter by department
- Filter by performance rating
- Filter by location
- Filter by experience

### 4. Correlation Analysis
```python
corr_matrix = correlation_analysis(df)
```
- Calculates correlation matrix for numerical variables
- Identifies relationships between:
  - Experience ↔ Salary
  - Age ↔ Salary
  - Performance ↔ Salary

### 5. Data Visualization

Six professional visualizations:

1. **Bar Chart** - Average salary by department
2. **Histogram** - Age distribution with mean/median lines
3. **Scatter Plot** - Experience vs Salary with trend line
4. **Pie Chart** - Employee distribution by department
5. **Box Plot** - Salary distribution by department
6. **Heatmap** - Correlation matrix

All charts are publication-quality (300 DPI, proper labels, clean styling).

### 6. Export Functionality
```python
export_filtered_data(df, 'filtered_results.csv')
export_summary_statistics(df)
```
- Save filtered datasets to CSV
- Export summary statistics to text file

## 📈 Sample Insights

**Key Findings from the Analysis:**

- **Average Salary:** $76,520
- **Highest Paying Department:** Engineering ($87,000 avg)
- **Strong Correlation:** Experience vs Salary (r = 0.85)
- **Workforce Composition:** 40% Engineering, balanced across others
- **Average Tenure:** 6.5 years in company
- **Top Performance Rating:** 4.9/5.0

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| **Python 3.8+** | Programming language |
| **Pandas** | Data manipulation and analysis |
| **NumPy** | Numerical computations and statistics |
| **Matplotlib** | Basic plotting and visualizations |
| **Seaborn** | Statistical data visualization |

## 📚 Documentation

- **[PROJECT_SCOPE.md](PROJECT_SCOPE.md)** - Detailed project objectives and tasks
- **[STEP_BY_STEP_GUIDE.md](STEP_BY_STEP_GUIDE.md)** - Complete implementation walkthrough
- **[INTERVIEW_QA.md](INTERVIEW_QA.md)** - Comprehensive interview preparation guide with 50+ Q&A

## 🎓 Learning Outcomes

This project demonstrates:

✅ **Pandas Skills:** Reading CSV, DataFrame operations, filtering, grouping
✅ **NumPy Skills:** Array operations, statistical calculations, polynomial fitting
✅ **Data Cleaning:** Handling dates, creating derived features, data type conversions
✅ **Data Analysis:** Descriptive statistics, correlation analysis, trend analysis
✅ **Data Visualization:** Creating meaningful charts with Matplotlib/Seaborn
✅ **Code Organization:** Writing modular, reusable, well-documented functions
✅ **Best Practices:** Error handling, docstrings, clean code structure

## 💼 Use Cases

This project is ideal for:

- **Job Applications:** Data Analyst, Junior Data Scientist roles
- **Portfolio Projects:** Showcase data analysis skills
- **Learning Resource:** Understand Pandas/NumPy best practices
- **Interview Preparation:** Practice explaining data analysis concepts
- **Template:** Starting point for similar analysis projects

## 🔧 Customization

### Using Your Own Data

1. Replace `employee_data.csv` with your dataset
2. Update column names in the script to match your data
3. Modify filters and analysis functions as needed

Example:
```python
# Change this:
df = load_data('employee_data.csv')

# To this:
df = load_data('your_data.csv')
```

### Adding New Analysis

The modular structure makes it easy to add new functions:

```python
def your_custom_analysis(df):
    """Your custom analysis description"""
    # Your code here
    pass

# Add to main():
def main():
    # ... existing code ...
    your_custom_analysis(df)
```

## 🤝 Contributing

Contributions are welcome! Here's how:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Saksham**
- Founder of Scult India
- Email: sg9935425@gmail.com
- LinkedIn: [Saksham's LinkedIn](https://www.linkedin.com/in/sakshamgupta036/)
- GitHub: [Saksham's GitHub](https://github.com/Sakshammp4)
- Youtube: [Saksham's Youtube](https://www.youtube.com/@SakshaM700X/videos)

## 🙏 Acknowledgments

- Dataset is synthetic and created for educational purposes
- Inspired by real-world HR analytics use cases
- Built as a learning project to demonstrate data analysis skills

## 📞 Contact

For questions, feedback, or collaboration opportunities:

- **Email:** sg9935425@gmail.com
- **GitHub Issues:** [Create an issue](https://github.com/yourusername/csv-data-analyzer/issues)

## ⭐ Show Your Support

If you found this project helpful, please give it a star! ⭐

---

**Happy Analyzing! 📊**

*Last Updated: January 2026*
