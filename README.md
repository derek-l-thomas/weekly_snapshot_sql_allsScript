# weekly_snapshot_sql_allsScript
Captures point in time (weekly) snapshots of engagement status and ladder engagement from leeds_new database (salesforce_contacts table), and records them in Google Sheet using Google Apps Script


**Project Documentation:**

**Summary of the Challenge:**
The challenge is to create a system that captures weekly snapshots of data regarding user engagement statuses and ladder engagement levels from a MySQL database. These snapshots are to be recorded in a Google Sheet for subsequent analysis and visualization in Tableau. The primary requirement is to ensure that the data for each week is consistently captured at the end of the week (Sunday at 11 PM) and reflects the status at that exact point in time.

**Overview of the Solution:**

To accomplish this task, we will:

1 - Create an SQL query that utilizes the CURRENT_DATE() function to fetch a snapshot of the current data.
2 - Use Google Apps Script to execute this SQL query against the database and write the results to a Google Sheet.
3 - Securely store database credentials within the Google Apps Script environment.
4 - Set up a time-driven trigger to run the script every Sunday night, capturing and recording the week's data.

**Detailed Steps:**

**Step 1: Writing the SQL Query**
Use the CURRENT_DATE() function to record the snapshot date.
Group data by engagement_status and ladder_engagement.
Count the number of records for each group.

SELECT 
    CURRENT_DATE() AS snapshot_date,
    IFNULL(engagement_status, 'NULL') AS engagement_status,
    IFNULL(ladder_engagement, 'NULL') AS ladder_engagement,
    COUNT(*) AS count
FROM 
    leeds_new.salesforce_contacts
GROUP BY 
    engagement_status, 
    ladder_engagement;

**Step 2: Setting Up Google Apps Script**
1 - Create a new Google Sheet which will be used to store the weekly data.
2 - Open the Google Apps Script editor from the Google Sheet by going to Extensions > Apps Script.
3 - Replace the placeholder code with the script that connects to the MySQL database and fetches data using the SQL query.

**Step 3: Securely Storing Credentials**
1 - In the Apps Script editor, go to File > Project properties > Script properties.
2 - Add new properties for DB_URL, DB_USER, and DB_PASS with the corresponding database URL, username, and password.

**Step 4: Script to Fetch Data and Write to Google Sheet**

function fetchWeeklySnapshot() {
  var scriptProperties = PropertiesService.getScriptProperties();
  
  var dbUrl = scriptProperties.getProperty('DB_URL');  
  var user = scriptProperties.getProperty('DB_USER');  
  var userPwd = scriptProperties.getProperty('DB_PASS'); 

  var conn = Jdbc.getConnection(dbUrl, user, userPwd);
  var stmt = conn.createStatement();
  var sql = `...`; // Your SQL code here
  // Rest of the script that processes and appends data to the Google Sheet
}

**Step 5: Scheduling the Script with a Trigger**
1 - Go back to the script editor and click on the clock icon (⏰) to open the triggers page.
2 - Click '+ Add Trigger' and configure it to run the fetchWeeklySnapshot function, time-driven, once a week, every Sunday, between 11 PM and midnight.

