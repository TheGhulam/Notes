## Open existing workbook

```python

import os
import openpyxl

os.chdir(<workbook folder>)

# Load workbook
workbook = openpyxl.load_workbook('example.xlsx')

#Check sheets
workbook.get_sheet_names()

#Load sheet
sheet = workbook.get_sheet_by_name(<sheet name>)

# Access cells
str(sheet['A1'].value)

{sheet.cell(row=1, column=2) # START AT 1
=
sheet['B1']}
```

## Create new workbook

```python
import openpyxl

wb = openpyxl.Workbook()
wb.get_sheet_names()
sheet = wb.get_sheet_by_name('Sheet')

# Save workbook to memory since now only in RAM
wb.save('example.xlsx')

# Create new sheets
wb.create_sheet(#optional:index=0, title='')

```


