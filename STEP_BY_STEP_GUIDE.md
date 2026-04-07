# Step-by-Step Guide: Building the CSV Data Analyzer

## 📚 Table of Contents
1. [Setup & Environment](#step-1-setup--environment)
2. [Import Libraries](#step-2-import-libraries)
3. [Load and Inspect Data](#step-3-load-and-inspect-data)
4. [Data Cleaning](#step-4-data-cleaning)
5. [Statistical Analysis](#step-5-statistical-analysis)
6. [Data Filtering](#step-6-data-filtering)
7. [Advanced Analysis](#step-7-advanced-analysis)
8. [Data Visualization](#step-8-data-visualization)
9. [Export Results](#step-9-export-results)
10. [Code Organization](#step-10-code-organization)
11. [Testing](#step-11-testing)
12. [GitHub Upload](#step-12-github-upload)

---

## Step 1: Setup & Environment

### 1.1 Create Project Directory
```bash
mkdir csv_data_analyzer
cd csv_data_analyzer
```

### 1.2 Create Virtual Environment (Optional but Recommended)
```bash
# Create virtual environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate
```

### 1.3 Install Required Libraries
```bash
pip install pandas numpy matplotlib seaborn
```

### 1.4 Create requirements.txt
```bash
pip freeze > requirements.txt
```

Or manually create with these contents:
```
pandas==2.0.3
numpy==1.24.3
matplotlib==3.7.2
seaborn==0.12.2
```

---

## Step 2: Import Libraries

Create `csv_analyzer.py` and start with imports:

```python
# csv_analyzer.py

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime
import warnings
warnings.filterwarnings('ignore')

# Set display options for better readability
pd.set_option('display.max_columns', None)
pd.set_option('display.width', None)
pd.set_option('display.max_rows', 20)
```

**Why these libraries?**
- **pandas:** Data manipulation and analysis
- **numpy:** Numerical operations and statistics
- **matplotlib:** Basic plotting
- **seaborn:** Advanced statistical visualizations
- **datetime:** Date calculations

---

## Step 3: Load and Inspect Data

### 3.1 Create Data Loading Function

```python
def load_data(file_path):
    """
    Load CSV file into a pandas DataFrame

    Parameters:
    file_path (str): Path to the CSV file

    Returns:
    pd.DataFrame: Loaded dataset
    """
    try:
        df = pd.read_csv(file_path)
        print(f"✅ Data loaded successfully!")
        print(f"Dataset shape: {df.shape[0]} rows, {df.shape[1]} columns\n")
        return df
    except FileNotFoundError:
        print(f"❌ Error: File '{file_path}' not found!")
        return None
    except Exception as e:
        print(f"❌ Error loading data: {e}")
        return None
```

### 3.2 Create Data Overview Function

```python
def data_overview(df):
    """Display comprehensive overview of the dataset"""

    print("="*70)
    print("📊 DATA OVERVIEW")
    print("="*70)

    # First few rows
    print("\n🔹 First 5 rows:")
    print(df.head())

    # Last few rows
    print("\n🔹 Last 5 rows:")
    print(df.tail())

    # Data info
    print("\n🔹 Dataset Information:")
    print(df.info())

    # Check for missing values
    print("\n🔹 Missing Values:")
    missing = df.isnull().sum()
    print(missing[missing > 0] if missing.sum() > 0 else "No missing values!")

    # Check for duplicates
    print(f"\n🔹 Duplicate Rows: {df.duplicated().sum()}")

    # Basic statistics
    print("\n🔹 Statistical Summary:")
    print(df.describe())

    print("\n" + "="*70 + "\n")
```

**Key Pandas Methods Used:**
- `head()`, `tail()`: View data samples
- `info()`: Get column types and non-null counts
- `isnull().sum()`: Count missing values
- `duplicated().sum()`: Find duplicate rows
- `describe()`: Generate descriptive statistics

---

## Step 4: Data Cleaning

### 4.1 Convert Date Column

```python
def clean_data(df):
    """Clean and preprocess the dataset"""

    print("🧹 Cleaning data...")

    # Convert JoinDate to datetime
    df['JoinDate'] = pd.to_datetime(df['JoinDate'])

    # Calculate years in company
    current_date = datetime.now()
    df['YearsInCompany'] = (current_date - df['JoinDate']).dt.days / 365.25
    df['YearsInCompany'] = df['YearsInCompany'].round(1)

    # Create age groups
    bins = [20, 25, 30, 35, 40, 50]
    labels = ['20-25', '26-30', '31-35', '36-40', '40+']
    df['AgeGroup'] = pd.cut(df['Age'], bins=bins, labels=labels, right=True)

    # Create salary categories
    df['SalaryCategory'] = pd.cut(df['Salary'],
                                   bins=[0, 60000, 80000, 100000, 150000],
                                   labels=['Entry', 'Mid', 'Senior', 'Executive'])

    print("✅ Data cleaning completed!\n")
    return df
```

**Key Operations:**
- `pd.to_datetime()`: Convert strings to datetime objects
- `pd.cut()`: Create categorical bins
- Date arithmetic for calculating tenure

---

## Step 5: Statistical Analysis

### 5.1 Overall Statistics

```python
def statistical_analysis(df):
    """Perform comprehensive statistical analysis"""

    print("="*70)
    print("📈 STATISTICAL ANALYSIS")
    print("="*70)

    # Salary statistics
    print("\n💰 SALARY STATISTICS:")
    print(f"Average Salary: ${df['Salary'].mean():,.2f}")
    print(f"Median Salary: ${df['Salary'].median():,.2f}")
    print(f"Salary Std Dev: ${df['Salary'].std():,.2f}")
    print(f"Min Salary: ${df['Salary'].min():,}")
    print(f"Max Salary: ${df['Salary'].max():,}")

    # Age statistics
    print("\n👥 AGE STATISTICS:")
    print(f"Average Age: {df['Age'].mean():.1f} years")
    print(f"Median Age: {df['Age'].median():.1f} years")
    print(f"Age Range: {df['Age'].min()} - {df['Age'].max()} years")

    # Experience statistics
    print("\n🎯 EXPERIENCE STATISTICS:")
    print(f"Average Experience: {df['YearsOfExperience'].mean():.1f} years")
    print(f"Median Experience: {df['YearsOfExperience'].median():.1f} years")

    # Performance statistics
    print("\n⭐ PERFORMANCE STATISTICS:")
    print(f"Average Rating: {df['PerformanceRating'].mean():.2f}")
    print(f"Median Rating: {df['PerformanceRating'].median():.2f}")

    print("\n" + "="*70 + "\n")
```

### 5.2 Department-wise Analysis

```python
def department_analysis(df):
    """Analyze data by department"""

    print("="*70)
    print("🏢 DEPARTMENT-WISE ANALYSIS")
    print("="*70)

    # Employee count by department
    print("\n📊 Employee Count by Department:")
    dept_count = df['Department'].value_counts()
    print(dept_count)

    # Average salary by department
    print("\n💵 Average Salary by Department:")
    avg_salary = df.groupby('Department')['Salary'].mean().sort_values(ascending=False)
    for dept, salary in avg_salary.items():
        print(f"{dept:15s}: ${salary:,.2f}")

    # Average experience by department
    print("\n📚 Average Experience by Department:")
    avg_exp = df.groupby('Department')['YearsOfExperience'].mean().sort_values(ascending=False)
    for dept, exp in avg_exp.items():
        print(f"{dept:15s}: {exp:.1f} years")

    # Average performance by department
    print("\n⭐ Average Performance Rating by Department:")
    avg_perf = df.groupby('Department')['PerformanceRating'].mean().sort_values(ascending=False)
    for dept, perf in avg_perf.items():
        print(f"{dept:15s}: {perf:.2f}")

    print("\n" + "="*70 + "\n")
```

**Key Pandas Methods:**
- `mean()`, `median()`, `std()`, `min()`, `max()`: Statistical functions
- `value_counts()`: Count unique values
- `groupby()`: Group data for aggregation
- `sort_values()`: Sort results

---

## Step 6: Data Filtering

### 6.1 Create Filter Functions

```python
def filter_by_salary(df, min_salary=None, max_salary=None):
    """Filter employees by salary range"""

    if min_salary and max_salary:
        filtered = df[(df['Salary'] >= min_salary) & (df['Salary'] <= max_salary)]
        print(f"Employees with salary between ${min_salary:,} and ${max_salary:,}:")
    elif min_salary:
        filtered = df[df['Salary'] >= min_salary]
        print(f"Employees with salary >= ${min_salary:,}:")
    elif max_salary:
        filtered = df[df['Salary'] <= max_salary]
        print(f"Employees with salary <= ${max_salary:,}:")
    else:
        return df

    print(f"Found {len(filtered)} employees\n")
    return filtered

def filter_by_department(df, department):
    """Filter employees by department"""

    filtered = df[df['Department'] == department]
    print(f"Employees in {department} department: {len(filtered)}\n")
    return filtered

def filter_by_performance(df, min_rating):
    """Filter employees by minimum performance rating"""

    filtered = df[df['PerformanceRating'] >= min_rating]
    print(f"Employees with performance rating >= {min_rating}: {len(filtered)}\n")
    return filtered

def filter_by_location(df, location):
    """Filter employees by location"""

    filtered = df[df['Location'] == location]
    print(f"Employees in {location}: {len(filtered)}\n")
    return filtered
```

**Filtering Techniques:**
- Boolean indexing: `df[condition]`
- Multiple conditions: `(cond1) & (cond2)`
- String matching: `df['col'] == value`
- Comparison operators: `>=`, `<=`, `==`

---

## Step 7: Advanced Analysis

### 7.1 Correlation Analysis

```python
def correlation_analysis(df):
    """Analyze correlations between numerical variables"""

    print("="*70)
    print("🔗 CORRELATION ANALYSIS")
    print("="*70)

    # Select numerical columns
    numerical_cols = ['Salary', 'Age', 'YearsOfExperience', 'PerformanceRating']

    # Calculate correlation matrix
    corr_matrix = df[numerical_cols].corr()

    print("\nCorrelation Matrix:")
    print(corr_matrix)

    # Find strongest correlations
    print("\n🔍 Key Findings:")

    exp_salary_corr = corr_matrix.loc['YearsOfExperience', 'Salary']
    print(f"Experience vs Salary correlation: {exp_salary_corr:.3f}")

    age_salary_corr = corr_matrix.loc['Age', 'Salary']
    print(f"Age vs Salary correlation: {age_salary_corr:.3f}")

    perf_salary_corr = corr_matrix.loc['PerformanceRating', 'Salary']
    print(f"Performance vs Salary correlation: {perf_salary_corr:.3f}")

    print("\n" + "="*70 + "\n")

    return corr_matrix
```

### 7.2 Top Performers Analysis

```python
def top_performers(df, n=10):
    """Identify top performers"""

    print("="*70)
    print(f"🌟 TOP {n} PERFORMERS")
    print("="*70)

    top = df.nlargest(n, 'PerformanceRating')[['Name', 'Department', 'Position',
                                                 'PerformanceRating', 'Salary']]
    print(top.to_string(index=False))
    print("\n" + "="*70 + "\n")

    return top
```

**Advanced Pandas Methods:**
- `corr()`: Calculate correlation matrix
- `nlargest()`, `nsmallest()`: Get top/bottom N rows
- Column selection: `df[['col1', 'col2']]`

---

## Step 8: Data Visualization

### 8.1 Setup Visualization Style

```python
def setup_plot_style():
    """Configure matplotlib and seaborn style"""

    plt.style.use('seaborn-v0_8-darkgrid')
    sns.set_palette("husl")
    plt.rcParams['figure.figsize'] = (10, 6)
    plt.rcParams['font.size'] = 10
```

### 8.2 Create Visualization Functions

```python
def visualize_salary_by_department(df):
    """Bar chart: Average salary by department"""

    plt.figure(figsize=(12, 6))

    avg_salary = df.groupby('Department')['Salary'].mean().sort_values(ascending=False)

    bars = plt.bar(avg_salary.index, avg_salary.values, color='steelblue', edgecolor='black')

    # Add value labels on bars
    for bar in bars:
        height = bar.get_height()
        plt.text(bar.get_x() + bar.get_width()/2., height,
                f'${height:,.0f}',
                ha='center', va='bottom', fontsize=10, fontweight='bold')

    plt.title('Average Salary by Department', fontsize=16, fontweight='bold', pad=20)
    plt.xlabel('Department', fontsize=12, fontweight='bold')
    plt.ylabel('Average Salary ($)', fontsize=12, fontweight='bold')
    plt.xticks(rotation=45, ha='right')
    plt.grid(axis='y', alpha=0.3)
    plt.tight_layout()
    plt.savefig('salary_by_department.png', dpi=300, bbox_inches='tight')
    plt.close()

    print("✅ Saved: salary_by_department.png")

def visualize_age_distribution(df):
    """Histogram: Age distribution"""

    plt.figure(figsize=(10, 6))

    plt.hist(df['Age'], bins=15, color='skyblue', edgecolor='black', alpha=0.7)

    plt.axvline(df['Age'].mean(), color='red', linestyle='--',
                linewidth=2, label=f'Mean: {df["Age"].mean():.1f}')
    plt.axvline(df['Age'].median(), color='green', linestyle='--',
                linewidth=2, label=f'Median: {df["Age"].median():.1f}')

    plt.title('Age Distribution of Employees', fontsize=16, fontweight='bold', pad=20)
    plt.xlabel('Age', fontsize=12, fontweight='bold')
    plt.ylabel('Frequency', fontsize=12, fontweight='bold')
    plt.legend()
    plt.grid(axis='y', alpha=0.3)
    plt.tight_layout()
    plt.savefig('age_distribution.png', dpi=300, bbox_inches='tight')
    plt.close()

    print("✅ Saved: age_distribution.png")

def visualize_experience_vs_salary(df):
    """Scatter plot: Experience vs Salary"""

    plt.figure(figsize=(12, 6))

    scatter = plt.scatter(df['YearsOfExperience'], df['Salary'],
                         c=df['PerformanceRating'], cmap='viridis',
                         s=100, alpha=0.6, edgecolors='black')

    # Add trend line
    z = np.polyfit(df['YearsOfExperience'], df['Salary'], 1)
    p = np.poly1d(z)
    plt.plot(df['YearsOfExperience'], p(df['YearsOfExperience']),
            "r--", linewidth=2, label='Trend Line')

    plt.colorbar(scatter, label='Performance Rating')

    plt.title('Experience vs Salary (colored by Performance)',
             fontsize=16, fontweight='bold', pad=20)
    plt.xlabel('Years of Experience', fontsize=12, fontweight='bold')
    plt.ylabel('Salary ($)', fontsize=12, fontweight='bold')
    plt.legend()
    plt.grid(alpha=0.3)
    plt.tight_layout()
    plt.savefig('experience_vs_salary.png', dpi=300, bbox_inches='tight')
    plt.close()

    print("✅ Saved: experience_vs_salary.png")

def visualize_department_distribution(df):
    """Pie chart: Employee distribution by department"""

    plt.figure(figsize=(10, 8))

    dept_counts = df['Department'].value_counts()

    colors = sns.color_palette('pastel')[0:len(dept_counts)]

    plt.pie(dept_counts.values, labels=dept_counts.index, autopct='%1.1f%%',
           startangle=90, colors=colors, explode=[0.05]*len(dept_counts),
           textprops={'fontsize': 11, 'fontweight': 'bold'})

    plt.title('Employee Distribution by Department',
             fontsize=16, fontweight='bold', pad=20)
    plt.tight_layout()
    plt.savefig('department_distribution.png', dpi=300, bbox_inches='tight')
    plt.close()

    print("✅ Saved: department_distribution.png")

def visualize_salary_boxplot(df):
    """Box plot: Salary distribution by department"""

    plt.figure(figsize=(12, 6))

    sns.boxplot(data=df, x='Department', y='Salary', palette='Set2')

    plt.title('Salary Distribution by Department',
             fontsize=16, fontweight='bold', pad=20)
    plt.xlabel('Department', fontsize=12, fontweight='bold')
    plt.ylabel('Salary ($)', fontsize=12, fontweight='bold')
    plt.xticks(rotation=45, ha='right')
    plt.grid(axis='y', alpha=0.3)
    plt.tight_layout()
    plt.savefig('salary_boxplot.png', dpi=300, bbox_inches='tight')
    plt.close()

    print("✅ Saved: salary_boxplot.png")

def visualize_correlation_heatmap(corr_matrix):
    """Heatmap: Correlation matrix"""

    plt.figure(figsize=(10, 8))

    sns.heatmap(corr_matrix, annot=True, fmt='.3f', cmap='coolwarm',
               center=0, square=True, linewidths=1, cbar_kws={"shrink": 0.8})

    plt.title('Correlation Heatmap', fontsize=16, fontweight='bold', pad=20)
    plt.tight_layout()
    plt.savefig('correlation_heatmap.png', dpi=300, bbox_inches='tight')
    plt.close()

    print("✅ Saved: correlation_heatmap.png")

def create_all_visualizations(df, corr_matrix):
    """Generate all visualizations"""

    print("\n🎨 Creating Visualizations...\n")

    setup_plot_style()

    visualize_salary_by_department(df)
    visualize_age_distribution(df)
    visualize_experience_vs_salary(df)
    visualize_department_distribution(df)
    visualize_salary_boxplot(df)
    visualize_correlation_heatmap(corr_matrix)

    print("\n✅ All visualizations created successfully!\n")
```

**Visualization Libraries:**
- `matplotlib.pyplot`: Basic plotting
- `seaborn`: Statistical visualizations
- Chart types: bar, histogram, scatter, pie, boxplot, heatmap

---

## Step 9: Export Results

### 9.1 Export Functions

```python
def export_filtered_data(df, filename):
    """Export filtered data to CSV"""

    df.to_csv(filename, index=False)
    print(f"✅ Exported {len(df)} rows to '{filename}'")

def export_summary_statistics(df):
    """Export summary statistics to text file"""

    with open('summary_statistics.txt', 'w') as f:
        f.write("="*70 + "\n")
        f.write("EMPLOYEE DATA ANALYSIS - SUMMARY STATISTICS\n")
        f.write("="*70 + "\n\n")

        f.write(f"Total Employees: {len(df)}\n\n")

        f.write("SALARY STATISTICS:\n")
        f.write(f"  Average: ${df['Salary'].mean():,.2f}\n")
        f.write(f"  Median: ${df['Salary'].median():,.2f}\n")
        f.write(f"  Min: ${df['Salary'].min():,}\n")
        f.write(f"  Max: ${df['Salary'].max():,}\n\n")

        f.write("DEPARTMENT DISTRIBUTION:\n")
        for dept, count in df['Department'].value_counts().items():
            f.write(f"  {dept}: {count}\n")

        f.write("\n" + "="*70 + "\n")

    print("✅ Exported summary statistics to 'summary_statistics.txt'")
```

---

## Step 10: Code Organization

### 10.1 Create Main Function

```python
def main():
    """Main function to run the analysis"""

    print("\n" + "="*70)
    print(" "*15 + "CSV DATA ANALYZER")
    print(" "*10 + "Employee/HR Data Analysis Tool")
    print("="*70 + "\n")

    # Load data
    df = load_data('employee_data.csv')

    if df is None:
        return

    # Data overview
    data_overview(df)

    # Clean data
    df = clean_data(df)

    # Statistical analysis
    statistical_analysis(df)
    department_analysis(df)

    # Correlation analysis
    corr_matrix = correlation_analysis(df)

    # Top performers
    top_performers(df, n=10)

    # Example filters
    print("\n📌 EXAMPLE FILTERS:\n")
    high_earners = filter_by_salary(df, min_salary=80000)
    eng_dept = filter_by_department(df, 'Engineering')
    top_rated = filter_by_performance(df, min_rating=4.5)

    # Create visualizations
    create_all_visualizations(df, corr_matrix)

    # Export results
    print("\n📤 EXPORTING RESULTS:\n")
    export_filtered_data(high_earners, 'high_earners.csv')
    export_summary_statistics(df)

    print("\n" + "="*70)
    print("✅ Analysis completed successfully!")
    print("="*70 + "\n")

if __name__ == "__main__":
    main()
```

---

## Step 11: Testing

### 11.1 Test Your Code

```bash
# Run the script
python csv_analyzer.py
```

### 11.2 Verify Outputs

Check for:
- ✅ Console output displays correctly
- ✅ 6 PNG image files created
- ✅ CSV export files created
- ✅ summary_statistics.txt created
- ✅ No errors in execution

---

## Step 12: GitHub Upload

### 12.1 Initialize Git Repository

```bash
git init
```

### 12.2 Create .gitignore

Create `.gitignore` file:
```
# Virtual environment
venv/
env/

# Python cache
__pycache__/
*.pyc
*.pyo

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db
```

### 12.3 Create README.md

(We'll create this in the next step)

### 12.4 Commit and Push

```bash
# Stage all files
git add .

# Commit
git commit -m "Initial commit: CSV Data Analyzer project"

# Create GitHub repository (via GitHub website)
# Then connect and push:
git remote add origin https://github.com/yourusername/csv-data-analyzer.git
git branch -M main
git push -u origin main
```

---

## 📝 Summary Checklist

- ✅ Environment setup complete
- ✅ Libraries imported
- ✅ Data loading function created
- ✅ Data cleaning implemented
- ✅ Statistical analysis functions built
- ✅ Filtering capabilities added
- ✅ Advanced analysis included
- ✅ 6 visualizations created
- ✅ Export functionality working
- ✅ Code organized and tested
- ✅ GitHub repository created

---

## 🎯 Next Steps

1. Test the code thoroughly
2. Add error handling
3. Create unit tests (optional)
4. Add command-line arguments (optional)
5. Prepare for interviews using INTERVIEW_QA.md

**Congratulations! You've built a complete data analysis project!** 🎉
