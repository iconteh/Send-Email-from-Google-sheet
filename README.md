# Send-Email-from-Google-sheet
Help me run this code.. i want to send email automatically from google sheet
//Automagically send emails using Google Sheets – April 2022
//elizabeth.kamara@tpisent.sl

function sendAssignment() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Schedule');
  var startRow = 2; // First row of data to process
  var numRows = sheet.getLastRow()-1; // Number of rows to process
  var dataRange = sheet.getRange(startRow, 1, numRows, sheet.getLastColumn()); // Fetch the range of cells being used A2:LastUsed
  var data = dataRange.getValues(); // Fetch values for each row in the Range.

  var templateText = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Template').getRange(1,1).getValue(); //Get template text from first cell in Template sheet
  var EMAIL_SENT = "EMAIL_SENT";

for (var i = 0; i < data.length; ++i) {
    var row = data[i];
    var date = new Date();
    var sheetDate = new Date(row[0]);

    //Make date formats the same for comparisson
    Sdate = Utilities.formatDate(date,"GMT+0′,’EEE, MMM d, yyyy")
    SsheetDate = Utilities.formatDate(sheetDate,"GMT+0′,’EEE, MMM d, yyyy")



    //Look through sheet for date in the first row that corresponds to today to build emails
    if (Sdate == SsheetDate){
      if (row[6] != EMAIL_SENT) { // Prevents sending duplicates
       var emailAddress = row[1];
       var subject = 'TpLearn Marketing Campaign';

       var Team = row[2];
       var Datemarketing  = row[3];
       var Type = row[4];
       var Location = row[5];

       var Date = Utilities.formatDate("Date of Marketing Campaign,’GMT+0′,’MMM d");


    // Another option for the email text is to concatinate it directly rather than use a template with replacement
    //var emailText = “Hello, this is a reminder that this Sunday ” + row[2] + “, ” + row[3] + ” has a ” + row[4]+ ” in Primary. This week’s theme is ” + row[5] + ” Thank you! The Primary Presidency”;


      //Replace the {STANDINS} in the template with the values assigned to variables from the Data Spreadsheet
      var emailText = templateText.replace('{Date of Marketing Campaign}', campaign).replace('{Team}',Team).replace('{Type of Marketing}', Marketing).replace('{Location}',Location);


      //Use the logger here to check that your template replacement has worked properly
      //Logger.log(emailText);

      //Send the mail – Once everything is set up properly, this next line is what sends the emails
      //MailApp.sendEmail(emailAddress, subject, emailText);

      //Add Email sent indication to end of row
      //sheet.getRange(startRow+i,7).setValue(“EMAIL_SENT”);


      //Email yourself to let you know what email was sent
      //Logger.log(‘SENT :’+emailAddress+’ ‘+subject+’ ‘+emailText)
      //var body = Logger.getLog();

     }
   }
MailApp.sendEmail('elizabeth.kamara@tpisent.sl','READ THIS!! – Sent Assignment' , body);
 }
}
