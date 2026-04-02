# How to Connect the Intake Form to Google Sheets

## Step 1: Create the Google Sheet
1. Go to sheets.google.com
2. Create a new spreadsheet
3. Name it "Review Removal Leads"
4. In Row 1, add these headers in order:
   A: Timestamp
   B: First Name
   C: Last Name
   D: Email
   E: Phone
   F: Business Name
   G: Client Type
   H: Services Needed
   I: Urgency
   J: Situation
   K: Budget
   L: Source URL

## Step 2: Create the Apps Script
1. In your Google Sheet, click Extensions > Apps Script
2. Delete all existing code
3. Paste this code:
```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    sheet.appendRow([
      data.timestamp,
      data.firstName,
      data.lastName,
      data.email,
      data.phone,
      data.businessName,
      data.clientType,
      data.services,
      data.urgency,
      data.situation,
      data.budget,
      data.source
    ]);
    return ContentService
      .createTextOutput(JSON.stringify({status: 'success'}))
      .setMimeType(ContentService.MimeType.JSON);
  } catch(error) {
    return ContentService
      .createTextOutput(JSON.stringify({status: 'error', message: error.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

## Step 3: Deploy the Apps Script
1. Click Deploy > New Deployment
2. Click the gear icon next to Type > Select Web App
3. Set Execute as: Me
4. Set Who has access: Anyone
5. Click Deploy
6. Copy the Web App URL

## Step 4: Paste the URL into index.html
1. Open index.html
2. Find the line: var SHEET_URL = 'PASTE_YOUR_APPS_SCRIPT_URL_HERE';
3. Replace PASTE_YOUR_APPS_SCRIPT_URL_HERE with your Web App URL

## Step 5: Test
Submit a test entry through the form on your site.
Check your Google Sheet - it should appear within seconds.
