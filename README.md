# CRM Data Cleaning Tool

A Python-based data cleaning tool designed to prepare CSV and Excel files for CRM imports, migrations, and integrations.

This project automates common data-cleaning tasks required before importing data into platforms such as HubSpot, Salesforce, NetSuite, and other CRM systems.

---

## Features

### Name Standardization

Supports multiple name formats:

| Original Value    | Result           |
| ----------------- | ---------------- |
| Doe, Jon          | Jon Doe          |
| DOE, JON          | Jon Doe          |
| jon doe           | Jon Doe          |
| Smith, Jane Marie | Jane Marie Smith |

Automatically creates:

* First Name
* Last Name
* Full Name

---

### Text Cleaning

Removes common data quality issues:

* Leading spaces
* Trailing spaces
* Multiple consecutive spaces
* Encoding artifacts
* Invalid special characters

Examples:

| Original     | Cleaned      |
| ------------ | ------------ |
| AcmeÂ Inc    | Acme Inc     |
| John   Doe   | John Doe     |
| Test Company | Test Company |

---

### Email Normalization

Converts email addresses to a consistent format:

| Original                                            | Cleaned                                             |
| --------------------------------------------------- | --------------------------------------------------- |
| [JOHN@COMPANY.COM](mailto:JOHN@COMPANY.COM)         | [john@company.com](mailto:john@company.com)         |
| [John.Doe@Company.Com](mailto:John.Doe@Company.Com) | [john.doe@company.com](mailto:john.doe@company.com) |

Features:

* Lowercase conversion
* Space removal
* Email-safe cleaning

---

### Phone Number Normalization

Converts phone numbers into a CRM-friendly format.

Examples:

| Original        | Cleaned     |
| --------------- | ----------- |
| 18457975194.0   | 18457975194 |
| (845) 797-5194  | 8457975194  |
| +1 845 797 5194 | 18457975194 |
| 1.8458E+10      | 18458000000 |

Features:

* Removes formatting characters
* Handles Excel scientific notation
* Preserves phone numbers as text
* Prevents decimal formatting issues

---

## Supported File Types

* CSV
* XLSX

---

## Installation

Clone the repository:

```bash
git clone https://github.com/socampo13/data-cleaner-from-file.git
cd data_cleaning.ipynb
```

Install dependencies:

```bash
pip install pandas openpyxl ftfy
```

---

## Usage

### Load a CSV File

```python
df = pd.read_csv("file.csv", dtype=str)
```

### Load an Excel File

```python
df = pd.read_excel("file.xlsx", dtype=str)
```

Using `dtype=str` is recommended to prevent:

* Phone number conversion
* Scientific notation issues
* Loss of leading zeros
* ID corruption

---

## Cleaning Process

The tool performs the following operations:

1. Load source file.
2. Clean text values.
3. Normalize names.
4. Generate First Name, Last Name, and Full Name fields.
5. Normalize email addresses.
6. Normalize phone numbers.
7. Generate a cleaned output file.

---

## Example Workflow

### Input

| Name       | Email                                       | Phone          |
| ---------- | ------------------------------------------- | -------------- |
| DOE, JON   | [JOHN@COMPANY.COM](mailto:JOHN@COMPANY.COM) | 18457975194.0  |
| Jane Smith | [Jane@Example.Com](mailto:Jane@Example.Com) | (845) 797-5194 |

### Output

| First Name | Last Name | Full Name  | Email                                       | Phone       |
| ---------- | --------- | ---------- | ------------------------------------------- | ----------- |
| Jon        | Doe       | Jon Doe    | [john@company.com](mailto:john@company.com) | 18457975194 |
| Jane       | Smith     | Jane Smith | [jane@example.com](mailto:jane@example.com) | 8457975194  |

---

## Use Cases

This tool is useful for:

* CRM migrations
* HubSpot imports
* Salesforce imports
* NetSuite integrations
* Marketing database cleanup
* Customer data standardization
* Data quality audits

---

## License

This project is licensed under the MIT License.

---

## Author

Developed to simplify CRM data preparation and improve data quality before system imports and integrations.
