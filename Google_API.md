## Data Engineering
<details> 
  <summary>Google Sheet API</summary>
  The official Google Application Programming Interface (API) enables interaction with various Google services.  This document focuses on using the API to interact with Google Sheets as a data source. 
</details>
<details>
  <summary>gspread</summary>
  gspread is a Python library that simplifies the process of interacting with Google Sheets.  Its purpose is to provide a user-friendly interface for reading, writing, and manipulating data within Google Sheets, abstracting away the complexities of the underlying Google Sheets API. 
</details>
<details>  
  <summary>Google Colab</summary>
  Google Colab is a free cloud-based Jupyter notebook environment that allows you to write and execute Python code in your browser.
</details>

## Google_API.ipynb
The objective of the python script is to automatically collate the transactions from each individual spreadsheet into a Single Source of Truth(SSOT). 
> [!IMPORTANT]
> A Service Account is required to run this script - Free to register for one.

> [!IMPORTANT]
> Google Sheet API must be activated from the Google Dev Console.

> [!IMPORTANT]
> Each individual spreadsheet must be shared with the service account.

### Importing Python Libraries
```
# Import Libraries
import json, re, datetime as dt
import pandas as pd, numpy as np

# Python library to access google sheets - https://docs.gspread.org/en/latest/
import gspread
import google.auth
from google.oauth2 import service_account
```

### Setting up Credentials
```
# Grab the Service Account Credentials from the JSON file
creds = service_account.Credentials.from_service_account_file('--insert .json file with Service Account Credentials--')

# Include the scope
scoped_creds = creds.with_scopes(['https://spreadsheets.google.com/feeds','https://www.googleapis.com/auth/drive'])

# authorize the clientsheet with gspread
client = gspread.authorize(scoped_creds)
```

### Filtering to our target spreadsheets
```
# Regular expression for matching spreadsheet - e.g. '[Jan'25] Living Expenses'
title_regex = re.compile(r"\[[A-Za-z][A-Za-z][A-Za-z]+'24+\] Living Expenses", re.IGNORECASE)
```
> Note: Only spreadsheet with the title containing '[XXX'24] Living Expenses' are selected


### Generate the list of spreadsheet objects, based on the above regex
```
# Handling of Multiple spreadsheet
spreadsheet_df_list = [] # An empty list

for spreadsheet in client.list_spreadsheet_files():
  if(title_regex.search(spreadsheet['name'])):
    print(spreadsheet['name'])

    # Opening the spreadsheet with matching name
    matching_sheet = client.open(spreadsheet['name'])

    print(matching_sheet.worksheets())

    # Select the 2nd worksheet 'Transactions' with the .worksheet method
    data_worksheet = matching_sheet.worksheet('Transactions')

    # Extract the data from cells B4:E100
    record_list = data_worksheet.get("B4:E100")

    # Slice the list into column header and row records
    col_header, col_data = record_list[0], record_list[1:]

    # Cast into a DataFrame for Data Engineering
    gSheetDF = pd.DataFrame(col_data, columns = col_header)

    # Remove '$' sign in the 'Amount' Column
    gSheetDF['Amount'] = gSheetDF['Amount'].str.slice(1)

    # Cast the DataFrame into the appropriate datatype
    gSheetDF = gSheetDF.astype({"Date": str, "Amount": float,
                          "Description": str, "Category": str})

    # Append each DataFrame into the 'spreadsheet_df_list' list
    spreadsheet_df_list.append(gSheetDF)
```

### Collating each spreadsheet into one single DataFrame
```
# Concat each DataFrame found in the list into one final DataFrame
final_df = pd.concat(spreadsheet_df_list, ignore_index=True)
display(final_df)
```

### Creates a placeholder Google Sheet to store our SSOT
```
# 1. Grab the spreadsheet shared with the Service Account
sheetname = 'Test_Sheet_0602' # Change this for testing
sheetDict = client.list_spreadsheet_files(sheetname)

if (len(sheetDict)) == 0:
  # 1a. If the spreadsheet doesn't exist
  # Creates the spreadsheet using the service account
  sh = client.create(sheetname)

  # Share the spreadsheet with my actual account - Set the role as "writer" first
  res = sh.share('--insert your main email account--', perm_type='user', role="writer", notify=True)

  # Retrieve the permission id to identify my account
  print(res.json()) # Display the content of the json file
  permissionId = res.json()["id"]

  # Transfer the ownership of the spreadsheet to my actual account
  sh.transfer_ownership(permissionId)

  # Now, I have to manually accept ownership of the spreadsheet - log in via gmail
  print(f'Please log in to your gmail account and accept ownership of the spreadsheet - {sheetname}')
else:
  # 1b. if the spreadsheet does exist
  # Open the spreadsheet
  sh = client.open(sheetname)

  # List all the permission associated with the spreadsheet
  print('Spreadsheet found! Listing all the associated permissions')
  for listing in sh.list_permissions():
    email, role = listing['emailAddress'], listing['role']
    print(f'Email: {email}')
    print(f'Role: {role}')
```

### Preparing the placeholder Google Sheet
```
# 2. Select the worksheet from the spreadsheet - expensesDataSheet
worksheet = sh.sheet1  # Or sh.worksheet("Sheet Name") if you want a specific sheet

# 3. Clear existing data in the selected sheet (optional but often useful)
worksheet.clear()
```

### Preparing the SSOT
```
# 4. Convert DataFrame to a list of lists (required by gspread)
data = [final_df.columns.values.tolist()] + final_df.values.tolist()  # Include header row
```

### Finalising the SSOT
```
# 5. Update the sheet with the DataFrame data, starting the cell 'A1'
worksheet.update(data, 'A1')
```
> Note: The end product is a Google Sheet containing all the transaction records.

