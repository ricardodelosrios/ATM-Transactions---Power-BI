# ATM-Transactions-Power-BI

<div style="display: inline_block"><br/>
  <img align="center" alt="Power BI" src="https://img.shields.io/badge/Power%20BI-61DBFB?style=for-the-badge&logo=Power%20BI&labelColor=black" />
<div style="display: inline_block"><br/>
 <img align="center" alt="Power Query" src="https://img.shields.io/badge/Power%20Query-Yellow"/>
 


https://github.com/ricardodelosrios/ATM-Transactions---Power-BI/assets/133066908/450b6148-2967-4b85-aab3-eeeae86c1f8e

**Link acceso:** [ATM Transaccions Power BI](https://app.powerbi.com/view?r=eyJrIjoiYjJhZjRjMDgtOWU2OC00YTEwLWE1ZDYtMjEwOThhNTY5MDcwIiwidCI6IjViMTU1MDU3LWMxMGEtNDM3Mi04NWU4LTEzZTA3ZGJlMTc3NSJ9).

# Introduction

Welcome to the data analytics project for a Bank in Nigeria. This project aims to analyze ATM transactions data to enhance customer experience and optimize operations. 

# Folders and files

* There is a 'Transaction' folder in this project:
  * This folder contains 5 CSV files which are the original databases used for the project, containing the ATM transactions of 5 states in Nigeria. The file names are listed below:
    * enugu_transactions.csv
    * fct_transactions.csv
    * kano_transactions.csv
    * lagos_transactions.csv
    * rivers_transactions.csv
  * There is an "Addicional tables" that will help develop the project:
    * atm_location_lookup.csv
    * CALENDAR_lookup.csv
    * customers_lookup.csv
    * hour_lookup.csv
    * transaction_type_lookup.csv
  * There is a folder call "images", where you will find the backgrounds of the dashboard:
    * Home Background.png
    * Demography Background.png
    * overview background.png
  * There is a file that explains what is in each column of the project files:
    * Data Dictionary.xlsx
  

# Data Loading

## Get Data:

* Open Power BI Desktop and select "Get Data" > "More" > "Folder: Transactions"
* Choose the folder containing the main tables, click "Combine," and select "Combine and Transform Data."

# Data Transformation with Power Query

## Transform Data:
* Click on "Transform Data" to open Power Query Editor.
* Add additional tables:
  * **atm_location_lookup.csv**
  * **CALENDAR_lookup.csv**
  * **customers_lookup.csv**
  * **hour_lookup.csv**
  * **transaction_type_lookup.csv**
## Table Renaming
* Rename additional tables:
 * Location
 * Calendar
 * Customer
 * Hour
 * Transaction Type
## Add Columns
### **Table "Transaction"**
  * **Duration**
    To calculate the transaction time in your dataset, follow these steps:
    1. Select the option to add a new column (`ADD COLUMN`).
    2. From the dropdown menu, choose the option to create a custom column (`CUSTOM COLUMN`).
    3. Assign a name to the new column, for example, "DURATION."
    4. In the custom column formula, use the following expression:
    ```
     Duration.TotalMinutes([TransactionEndDateTime]-[TransactionStartDateTime])
    ```
  * **Extracting Transaction Start Time**

    To extract only the hour at which the transaction started, follow these steps:

    1. Click on the "TransactionStartDateTime" column.
    2. Select the option to add a new column (`Add Column`).
    3. Choose the option for extracting time (`Time`).
    4. Specify that you want to extract the hour (`Hour`).
      
### **Table "Customers"**
  * **Calculating Customer Age in the "Customers" Table**

    In the "Customers" table, we will calculate the age of the customers. To do this, follow these steps:

    1. Add a new column (`ADD COLUMN`).
    2. Choose the option to create a custom column (`CUSTOM COLUMN`).
    3. Set the new column name as "Age."
    4. In the custom column formula, use the following expression:

   ```
   Duration.TotalDays(#date(2023,1,1) - [Birth Date]) / 365.25
   ```
  **Create Age Groups in a New Column**

   To categorize ages into groups in your dataset, follow these steps using your data analysis tool:

   1. Select the option to add a new column (`ADD COLUMN`).
   2. Choose the option to create a conditional column (`CONDITIONAL COLUMN`).
   3. Set up the conditional column as follows:

   - **Column Name:** Age
   - **Operator:** is less than or equal to
   - **Value:** 15
   - **Output:** 0-15

   5. Repea Repeat this process for the ranges 16-34, 26-35, 36-45, 46-55, and 56-65, adjusting values and outputs as needed.

   6. For the last range, set up the conditional column as follows:

   - **Column Name:** Age
   - **Operator:** is greater than
   - **Value:** 65
   - **Output:** More than 65

# Data Modeling

 * Change the name of the "TransactionStartDateTime" column to "Date" for proper relationships.

## Setting Up Database Relationships

* Open the **"Model View,"** select the "Manage Relationships" option to delete all existing relationships and start from scratch, ensuring that the relationships are configured correctly.
* Now, let's create the new relationships:
   1. Click on **"New,"** choose the primary table as **"Transactions,"** and establish a relationship with the **"Calendar"** table by selecting the **"date"** column in both tables.
   2. Click on **"New,"** choose the primary table as **"Transactions,"** and establish a relationship with the **"Customers"** table by selecting the **"CardholderID"** column in both tables.
   3. Click on **"New,"** choose the primary table as **"Transactions,"** and establish a relationship with the **"Hour"** table by selecting the **"Hour"** column in one table and the **"hour_key"** column in the other.
   4. Click on **"New,"** choose the primary table as **"Transactions,"** and establish a relationship with the **"Location"** table by selecting the **"LocationID"** column in both tables.
   5. Click on **"New,"** choose the primary table as **"Transactions,"** and establish a relationship with the **"Transaction Type"** table by selecting the **"TransactionTypeID"** column in both tables.
 
  ![alt text](https://github.com/ricardodelosrios/ATM-Transactions---Power-BI/blob/main/Images/Database%20relationships.png)

  ## Create Calculated Table and Measures

  1. Set Up "Report View"
   Switch the view to "Report view."

  2. Create a New Table
   Navigate to the "Modeling" tab, select "New Table," and enter the following formula:
   ```
   [Measures Table] = {Blank()}
    ```
   3. Create Average Transaction Amount Measure
    To address the question from the project brief, "What is the average transaction amount by location and transaction type?," follow these steps:

     * Select the "Measures Table."
     * Click on the three dots (...) and choose "New Measure."
     * Enter the following formula:
    ```
    average_amount = AVERAGE(Transactions[TransactionAmount])
    ```
   4. Create Transaction Amount Measure Over Time
   To address the question regarding transaction volume and amount trends over time, and identifying seasonal patterns, follow these steps:

    * Select the "Measures Table."
    * Click on the three dots (...) and choose "New Measure."
    * Enter the following formula:
    ```
    transaction_amount = SUM(Transactions[TransactionAmount])
    ```
    5. Create Measures for Average Transaction Amount and Frequency
    To answer the question, "What is the average transaction amount and transaction frequency per customer by occupation and age group?," create two measures:

    ```
    number_of_customers = DISTINCTCOUNT(Transactions[CardholderID])
    ```
    ```
    transaction_frequency = DIVIDE([transactions_count], [number_of_customers])
    ```
    6. Utilization Rate Measure
    For the question "Which ATM locations have the highest and lowest utilization rates, and what factors contribute to this utilization rate?," create the following measure:
    ```
    
    Utilization Rate = 

    VAR transaction_time = SUM(Transactions[Duration])
    VAR available_time = 24 * 365 * 60 * SUM(Location[No of ATMs])
    VAR utilization_rate = DIVIDE(transaction_time, available_time)

    RETURN
    utilization_rate
    ```
    Explanation:

    transaction_time: Sum of "duration" in the "Transactions" table.
    available_time: Multiplication of hours (24), days in a year (365), minutes per hour (60), and the sum of ATMs.
    utilization_rate: Division of the above two variables.

    7. Average Transaction Time Measure
    To address the question "What is the average transaction time by location, transaction type, and time of day, and how does it vary by customer type and occupation?," create the following     measure:

    ```
    average_duration = AVERAGE(Transactions[Duration])
    ```
    8. Percentage of Transactions Measure
    Create a new measure to calculate the percentage of transactions:
    ```
    % Transactions = 
    DIVIDE([transactions_count],
        CALCULATE([transactions_count], ALLSELECTED(Transactions))
    )
    ```
    Explanation:

    * [transactions_count]: Represents the measure or column containing the count of transactions under consideration (numerator).
    * CALCULATE([transactions_count], ALLSELECTED(Transactions)): Calculates the total number of transactions but with a modified filter context. ALLSELECTED(Transactions) removes all filters applied in the Transactions table while keeping filters applied in other tables.
    In summary, this formula calculates the percentage of transactions by dividing the count of transactions in consideration by the total count of transactions, considering a specific filter context for the Transactions table. This is useful when calculating percentages in relation to the total while selectively handling the filter context.
    
    9. Count of Transactions Measure
    Create a new measure to count the number of transactions:
    ```
    transactions_count = COUNTROWS(Transactions)
    ```

  # Visualization

    The project is organized into three main pages:
    
    ## 1. Home Page
    - The home page provides an overview of the project.
    - It includes the project name and navigation buttons to access other dashboard pages.
    - Offers an intuitive experience for users who want to explore different sections of the analysis.
    
    ## 2. Overview Page
    - The "Overview" page focuses on the analysis of ATM transactions.
    - It provides detailed visualizations, charts, and reports on transactions, offering a comprehensive understanding of patterns and trends.
    
    ## 3. Demographics Page
    - The "Demographics" page concentrates on demographic analysis related to transactions.
    - It includes charts and reports displaying the demographic distribution of users and its impact on ATM transactions.
  










    
 
  
  
