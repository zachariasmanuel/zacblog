+++
date = "2018-12-19T11:30:00+05:30"
title = "Extract email IDs from Gmail"
tags = ["Email id extract" , "Gmail", "Email extract", "Google app script", "Google script", "Email scanner", "scan email", "zac"]
+++


Hey people! Writing after a long time. Today I will explain how to scan your Gmail and extract all email IDs to a Google spreadsheet using Google apps script.

1\. Go to google drive, create a new spreadsheet and give it a name.

2\. Open the script editor. Tools -> Script Editor

3\. Copy and paste the below code to the script editor and save the script with a name.


```javascript
var ss = SpreadsheetApp.getActiveSpreadsheet();
var sheet = ss.getActiveSheet();

// add menu to Sheet
function onOpen() {
    var ui = SpreadsheetApp.getUi();
    ui.createMenu('Extract Emails')
        .addItem('Extract emails from inbox', 'extractEmailFromInbox')
        .addItem('Extract emails from label', 'extarctEmailFromLablel')
        .addToUi();
}

function extractEmailFromInbox(){
  var threads = GmailApp.getInboxThreads();
  extractEmails(threads);
}

function extarctEmailFromLablel(){
  var label = sheet.getRange(1, 1).getValue();
  var threads = GmailApp.search ("label:" + label);
  extractEmails(threads);
}

function extractEmails(threads) {
    var messages = GmailApp.getMessagesForThreads(threads);
    var emailArray = [];

    // get array of email addresses
    messages.forEach(function(message) {
        message.forEach(function(d) {
            emailArray.push(d.getFrom());
        });
    });

    // de-duplicate the array
    var uniqueEmailArray = emailArray.filter(function(item, pos) {
        return emailArray.indexOf(item) == pos;
    });

    //Clean email to seperate email and name
    var cleanedEmailArray = uniqueEmailArray.map(function(el) {
        var name = "";
        var email = "";
        var matches = el.match(/\s*"?([^"]*)"?\s+<(.+)>/);

        if (matches) {
            name = matches[1];
            email = matches[2];
        } else {
            name = "N/k";
            email = el;
        }
        return [name, email];
    }).filter(function(d) {
        if (
            d[1] !== "zac@zachariasmanuel.com" &&
            d[1] !== "drive-shares-noreply@google.com" &&
            d[1] !== "mailer-daemon@googlemail.com"
        ) {
            return d;
        }
    });

    //Show alert if there is no email
    if (cleanedEmailArray.length == 0) {
        var ui = SpreadsheetApp.getUi();
        var result = ui.alert(
            'Alert!',
            'There is no email.',
            ui.ButtonSet.OK);
    } else {
        sheet.getRange(3, 1, cleanedEmailArray.length, 2).setValues(cleanedEmailArray).sort(2);
    }
}
```
![EE2](/img/email_extract_2.png)

4\. Return to the spreadsheet, refresh it and a new menu item will appear on top of the spreadsheet as shown in the image below.

![EE1](/img/email_extract_1.png)


5\. To scan your entire inbox, click on 'Extract emails from inbox' (from the new menu item) and wait for a few minutes. The response time depends on the number of emails in your inbox. This will fetch you the scan result into your spreadsheet. 

6\. You can also scan a label for email IDs. For this, enter the name of the label that you want to scan in the cell 'A1'. Click on 'Extract emails from label'. This scans all the emails marked in that label and extracts the email IDs to the spreadsheet.

Find the github repository [here](https://github.com/zachariasmanuel/EmailIdExtractor). Your contributions are welcome.

You can also mark your issues [here] (https://github.com/zachariasmanuel/EmailIdExtractor/issues).

✌️