# Convert data from YDOC to MySQL


Overview
This code processes CSV files located in a specified folder, merges their data into a single DataFrame, renames the columns, and then inserts the processed data into a MySQL database.

Code Breakdown
Import Libraries:

The code imports necessary libraries:
pandas for data manipulation and analysis.
os for interacting with the operating system (like reading files).
mysql.connector for connecting to and interacting with a MySQL database.
Function to Convert Date Format:

convert_date_format(date_series): This function takes a series of dates and converts them from the format DD/MM/YYYY to YYYY/MM/DD.
Function to Process CSV Files:

process_csv_files(file_path):
Initializes a list to store DataFrames.
Defines new column names for the first 15 columns.
Iterates through all CSV files in the specified directory.
For each CSV file:
Reads the file into a DataFrame.
Drops the first two rows (usually headers or unwanted data).
Converts the 'Date' column to a proper date format if needed.
Merges 'Date' and 'Time' columns into a new 'DateTime' column.
Drops the original 'Date' and 'Time' columns.
Reorders columns to place 'DateTime' first.
Renames the first 15 columns according to predefined names.
Appends the processed DataFrame to the list.
Concatenates all DataFrames into one.
Drops any columns that have all NaN values.
Converts all columns to numeric types except for the first column (Timestamp).
Returns the final processed DataFrame.
Function to Insert Data into MySQL:

insert_data_to_mysql(all_data, db_name):
Establishes a connection to the MySQL server.
Creates a database (if it doesn't exist) and selects it.
Creates a table named YDOC with specified columns (data types defined).
Prepares to insert data into the table:
Replaces spaces in column names with underscores for SQL compatibility.
Drops rows with NaN values from the DataFrame.
Generates a dynamic SQL insert query based on the DataFrame's columns.
Iterates through each row of the DataFrame and inserts it into the YDOC table.
Commits the changes to the database.
Closes the database connection.
Main Function:

main():
Defines the path where the CSV files are located.
Calls the process_csv_files function to read and process the CSV files.
Calls the insert_data_to_mysql function to insert the processed data into the MySQL database.

Execution:

The last lines check if the script is being run directly. If so, it calls the main() function to execute the process.

Summary
Reads all CSV files in a specified directory.
Processes each file by cleaning and transforming the data.
Renames columns and merges the data into a single DataFrame.
Inserts the final DataFrame into a MySQL database table named YDOC.
This code automates the workflow of handling CSV data and ensures it is stored correctly in a relational database for further analysis or reporting.


Code to see the data from SQL command line
USE YDOCDatabase
DESCRIBE YDOC
SELECT * FROM YDOC;