+++
date = "2018-12-27T12:15:00+05:30"
title = "Create CSV file from Google Spreadsheet"
tags = ["CSV creator" , "Spreadsheet", "Email CSV", "Google app script", "Google script", "Create file in Google drive", "zac"]
+++


Hello! It is very easy to create a CSV file from data in a Google spreadsheet using Google Apps Script. I have written this code for creating CSV file with email IDs to import in Google groups as it is very difficult to copy paste the emails IDs manually. The aim of this post is to explain how to create files and folders using Google script.

1\. Open your spreadsheet that contains the data

![EE1](/img/CSV_create_2.png)

2\. Open the script editor. Tools -> Script Editor

3\. Copy and paste the below code to the script editor and save the script with a name.


```javascript
var fileName = 'output.csv';
var folderName = 'EmailCSV';
var column = 0;
var startingRow = 0;

function createCSV() {
  deleteFolder();
  //var sss = SpreadsheetApp.openById('17KItHQiT1urUwovcTZ9EWsHhEfINycugWmfT_oQ');
  //var ss = sss.getSheetByName('data');
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getActiveSheet();

  var range = ss.getDataRange();
  var data = range.getValues();

  var finalData = "";
  for(i = startingRow; i < data.length; i++){
    if(finalData == ""){
      finalData = data[i][column];
    }
    else{
      finalData = finalData + "," +data[i][column];
    }
  }
  writeFile(finalData);
}

function writeFile(data){
  Logger.log(data);
  var folder = DriveApp.createFolder(folderName);
  var file = folder.createFile(fileName, data, MimeType.PLAIN_TEXT); 
}

function deleteFolder(){
  var folder=DriveApp.getFoldersByName(folderName).next();
  if(folder){
    DriveApp.removeFolder(folder);
  }
}
```

4\. Select the function 'createCSV', run the code and authorize the code to run.

![EE1](/img/CSV_create_1.png)


5\. Open your google drive. You will find a folder named 'EmailCSV' and a file named 'output.csv'. Download the file and use it.

![EE1](/img/CSV_create_3.png)

6\. You can change the folder name and file name by editing the code. You can also change the column to scan and starting row.

Find the github repository [here](https://github.com/zachariasmanuel/CSVCreator). Your contributions are welcome.

You can also mark your issues [here] (https://github.com/zachariasmanuel/CSVCreator/issues).
