# Wellsky to Adams Keegan Payroll Converter

A simple static web application that converts Wellsky payroll Excel files to Adams Keegan format. This application runs entirely in the browser with no backend required.

## Features

- **File Upload**: Drag-and-drop or browse to upload Wellsky Excel files (.xlsx, .xls)
- **SSN Management**: Import SSNs from Google Sheets with support for multiple formats
- **Data Conversion**: Automatically converts payroll data following Adams Keegan requirements
- **Editable Preview**: Review and edit converted data before download
- **Excel Export**: Download converted data as Excel file ready for Adams Keegan import

## How to Use

### Step 1: Upload Wellsky Excel File
1. Drag and drop your Wellsky Excel file onto the upload area, or click to browse
2. The application will parse the file and extract employee data
3. You'll see confirmation of how many employee records were processed

### Step 2: Import SSNs
1. Copy SSN data from Google Sheets and paste into the textarea
2. Supports multiple formats:
   - Tab-separated: `Name [tab] SSN`
   - Dash-separated: `Name - SSN`
   - Comma-separated: `Name, SSN`
3. Click "Import SSNs" to process the data
4. Use "View Current SSNs" to see loaded data
5. Use "Clear All" to remove all SSNs

### Step 3: Preview & Download
1. Review the converted data in the editable table
2. Edit any fields as needed (especially SSNs)
3. Add new employees or delete rows as required
4. Click "Download Excel File" to get the Adams Keegan format file

## Conversion Rules

The application follows these critical conversion rules:

- **Columns H-N are always "0"** to prevent double-counting in Adams Keegan
- **Hours are grouped by base rate** per employee (separate row for each rate)
- **Miles**: Only from "Per Mile" method entries, placed on first row
- **Expense reimbursement**: Only from "Not Payable" method entries, placed on first row
- **Zero-hour employees**: If employee has only mileage/expenses (no hours), creates row with zeros for hours

## Adams Keegan Output Format

The output Excel file contains these columns in exact order:

1. Caregiver
2. SSN (auto-filled from imported SSNs)
3. Total Hours
4. Reg Hours
5. OT (1.5x)
6. DOT (2x)
7. Miles
8. Holiday (always 0)
9. Hourly (1.5X) (always 0)
10. Live In Hours (always 0)
11. Live In/Hourly (always 0)
12. Per Visit (always 0)
13. Holiday Live In/Hourly (1.5X) (always 0)
14. No of visit (always 0)
15. Base Rate
16. Method
17. Expense reimbursement

## Local Development

To run the application locally:

1. Clone this repository
2. Open `index.html` in your web browser
3. No build process or server required

## Deployment to Heroku

### Prerequisites
- Git installed
- Heroku CLI installed
- GitHub account

### Step 1: Initialize Git Repository

```bash
cd wellsky-converter
git init
git add .
git commit -m "Initial commit: Wellsky to Adams Keegan converter"
git branch -M main
```

### Step 2: Create GitHub Repository

1. Go to GitHub and create a new repository
2. Copy the repository URL
3. Add GitHub remote:

```bash
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

### Step 3: Deploy to Heroku

```bash
# Create Heroku app (replace with your preferred name)
heroku create wellsky-converter-YOUR_NAME

# Set PHP buildpack
heroku buildpacks:set heroku/php

# Deploy to Heroku
git push heroku main

# Open the application
heroku open
```

### Step 4: Enable Automatic Deployments (Optional)

1. Go to your Heroku dashboard
2. Select your app
3. Go to "Deploy" tab
4. Connect to GitHub
5. Enable automatic deploys from main branch

## Technical Details

- **Frontend**: Pure HTML, CSS, JavaScript (no frameworks)
- **Excel Processing**: SheetJS (XLSX) library from CDN
- **Styling**: Bootstrap 5 from CDN
- **Deployment**: Heroku with PHP buildpack
- **No Backend**: All processing happens client-side
- **No Database**: Data exists only in memory during session

## File Structure

```
wellsky-converter/
├── index.html          # Complete single-page application
├── index.php           # Redirect to index.html for Heroku
├── composer.json       # Empty JSON for PHP buildpack
├── .gitignore          # Git ignore file
└── README.md           # This file
```

## Testing Checklist

Before deploying, test these scenarios:

- [ ] Upload Wellsky Excel file
- [ ] Paste SSNs and import successfully
- [ ] Verify conversion (columns H-N are zero)
- [ ] Verify miles and expenses on correct rows
- [ ] Edit fields in preview table
- [ ] Add new employees
- [ ] Delete employees
- [ ] Download Adams Keegan Excel file
- [ ] Import downloaded file into Adams Keegan (verify no double counting)

## Troubleshooting

### File Upload Issues
- Ensure file is .xlsx or .xls format
- Check that file contains proper Wellsky format data
- Try refreshing the page and uploading again

### SSN Import Issues
- Verify SSN format (9 digits)
- Check separator format (tab, dash, or comma)
- Ensure name matches exactly with Excel file

### Conversion Issues
- Verify Wellsky file has proper structure
- Check that employee names match SSN names
- Ensure method names are correct ("Per Mile", "Not Payable")

## Support

This application is designed to be self-contained and easy to use. If you encounter issues:

1. Check the browser console for errors
2. Verify your input files match the expected format
3. Try refreshing the page and starting over
4. Ensure you're using a modern web browser

## License

This project is open source and available under the MIT License.
