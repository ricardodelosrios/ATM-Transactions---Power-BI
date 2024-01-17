# ATM-Transactions-Power-BI

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










    
 
  
  
