# HR ANALYTICS DASHBOARD

## 📌 Table of Contents
1. [Project Overview](#1-project-overview)
2. [Business Problem](#2-business-problem)
3. [Data Sources](#3-data-sources)
4. [Data Cleaning & Transformation (Power Query)](#4-data-cleaning--transformation-power-query)
5. [Data Modeling](#5-data-modeling)
6. [DAX Measures Created](#6-dax-measures-created)
7. [Dashboard Design & Visuals](#7-dashboard-design--visuals)
   - [Page 1: Overview](#page-1-overview)
   - [Page 2: Attrition](#page-2-attrition)
   - [Page 3: Employee Details](#page-3-employee-details)
8. [Key Insights](#8-key-insights)
9. [Tools Used](#9-tools-used)
10. [Project Deliverables](#10-project-deliverables)
11. [Live Dashboard Link](#11-live-dashboard-link)

---

## 1. Project Overview

This report was designed for HR Executives who want a quick, reliable, and intuitive way to understand what’s happening within their workforce.  
Instead of digging through spreadsheets or jumping between HR systems, the dashboard brings everything together into one interactive view.

The project includes three pages:

- **Overview:** A high-level snapshot of the organization’s workforce.  
- **Attrition:** A deeper dive into why employees leave and who leaves the most.  
- **Employee Details:** A full HR database, fully filterable and cleanly structured for quick reference.

**My goal was simple:**  
👉 *Turn raw HR data into a story — one that helps leadership make smarter decisions about people.*

---

## 2. Business Problem

HR teams often struggle with keeping track of employee trends over time — attrition patterns, headcount changes, age demographics, hiring timelines, and departmental distribution.  
The data usually sits across different files, different formats, and different levels of completeness.

This makes it harder for HR leaders to answer simple but important questions:

- Are we losing more employees this year?  
- Which departments are struggling with turnover?  
- What does our workforce actually look like?  
- Are we hiring or losing talent faster than expected?

This dashboard solves that by centralizing everything into one consistent, automated, and interactive report that HR leadership can rely on for accurate workforce insights.

---

## 3. Data Sources

The project uses a single HR dataset containing:

- Employee personal details  
- Positions & Departments  
- Date of Hire  
- Date of Termination  
- Employment Status  
- Salary  
- Demographic details (Gender, Race, Age)

This dataset was cleaned and shaped in Power Query before modeling in Power BI.

---

## 4. Data Cleaning & Transformation (Power Query)

The data preparation phase was hands-on and intentional.  
I focused on making the dataset clean, consistent, and analysis-ready.

**Key steps included:**

- Removed unnecessary or irrelevant columns that didn't contribute to the analysis.  
- Renamed several columns for clarity and consistency (e.g., DOB, DateofHire, EmploymentStatus).  
- Corrected data types — especially dates, text fields, and numeric columns.  
- Created a Date Table covering **1 Jan 2006 – 31 Dec 2018**  
  This supported both Date of Hire and Date of Termination.  

**Extracted time intelligence fields**
- Year  
- Month number  
- Month name  

**Added Age and Age Band columns** by calculating the employee’s age from Date of Birth, then grouping them into:

- 33–39  
- 40–49  
- 50–59  
- 60–74  

Ensured relationships remained clean and avoided ambiguity.

This gave me a rock-solid foundation for modeling and DAX.

---

## 5. Data Modeling

The model was built around a simple, efficient **star schema**:

### **Fact Table**
- Employee Records (core HR data)

### **Dimension Tables**
- Date Table  
- Position  
- Department  
- Age Band  

A unique challenge was the need to calculate attrition using Date of Termination — a relationship that isn’t active by default, so I used **USERELATIONSHIP** to activate it only when calculating attrition-specific measures.

```dax
Terminated Employees =
CALCULATE(
    [Total Employees],
    HRDataset[EmploymentStatus] <> "Active",
    USERELATIONSHIP('Date Table'[Date], HRDataset[DateofTermination])
)
```
---

## 6. DAX Measures Created

I created a dedicated Measures Table to keep calculations organized.

### **Core HR Metrics**
- Total Employees  
- Average Salary  
- Active Employees  
- Terminated Employees (via USERELATIONSHIP)  
- Attrition Rate  

### **Support Metrics**
- Headcount by Department  
- Termination Count by Reason  
- Employees by Age Band / Race / Sex  

These measures powered the visuals and shaped the story behind the dashboard.

---

## 7. Dashboard Design & Visuals

### Page 1: Overview
This page answers the big questions instantly:

- Total Employees  
- Average Salary  
- Attrition Rate  
- Employees by Gender  
- Citizenship  
- Marital Status  
- Department distribution  
- Workforce age brackets  
- Racial diversity  

<img width="1027" height="560" alt="HR 1" src="https://github.com/user-attachments/assets/3d5be22f-3f85-4e9d-bce0-ad9167c63401" />

---

### Page 2: Attrition
This page focuses on employee turnover:

- Terminated vs Active employees  
- Attrition by Gender  
- Attrition Trend by Year  
- Termination Reasons ranked  
- Department-level attrition  

<img width="1022" height="560" alt="HR 2" src="https://github.com/user-attachments/assets/86749b35-0b03-49ae-a1b0-bae55e5be73e" />

---

### Page 3: Employee Details
A clean table for HR executives to quickly find any employee:

- Employee ID  
- Name  
- Sex  
- Date of Birth  
- Citizenship  
- Department  
- Date of Hire  
- Age Band  
- Employment Status  

<img width="1016" height="558" alt="HR 3" src="https://github.com/user-attachments/assets/6bae09e6-f121-4e27-80aa-54711552af57" />


---

## 8. Key Insights

- The organization has **311 total employees**, with an **average salary of $69K**.  
- Female employees make up a smaller share of the workforce.  
- The department with the largest headcount is **Production** with over 200 employees.  
- Attrition rate sits at **50%**, driven mainly by:  
  - “Another position”  
  - “Unhappy”  
  - “More money”  
- Age distribution shows the largest group falls between **40–49 years**.  
- The attrition trend shows a sharp spike in recent years, requiring leadership attention.

---

## 9. Tools Used

- Power BI Desktop  
- Power Query  
- DAX  
- Excel  

---

## 10. Project Deliverables

- A fully interactive 3-page HR Dashboard  
- Cleaned and transformed HR dataset  
- Dynamic Date Table  
- Organized DAX Measures Table  
- Documentation for GitHub portfolio  

---

## 11. Live Dashboard Link
[Click to View the Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiZTY1NWEzNjQtNWE5YS00Y2NjLWFkM2YtYTU2MDUyMzc0OThhIiwidCI6IjJiYjFlMzEyLTIwN2QtNDUyYi05OGRhLTE0MTc2MmIxMWJjZiJ9)
