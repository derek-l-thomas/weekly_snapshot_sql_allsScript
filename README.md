# weekly_snapshot_sql_allsScript
Captures point in time (weekly) snapshots of engagement status and ladder engagement from leeds_new database (salesforce_contacts table), and records them in Google Sheet using Google Apps Script

**Overview of the Solution:**

1) Create an SQL query that utilizes the CURRENT_DATE() function to fetch a snapshot of the current data.
2) Use Google Apps Script to execute this SQL query against the database and write the results to a Google Sheet, and sets up a time-driven trigger to run the script every Sunday night, capturing and recording the week's data.

**Detailed Steps:**

**Step 1: Writing the SQL Query**
Uses the CURRENT_DATE() function to record the snapshot date. Groups data by engagement_status and ladder_engagement. Counts the number of records for each group.

**Step 2: Setting Up Google Apps Script**
1 - Create a new Google Sheet which will be used to store the weekly data.
2 - Open the Google Apps Script editor from the Google Sheet by going to Extensions > Apps Script.
3 - Replace the placeholder code with the script that connects to the MySQL database and fetches data using the SQL query.

**Step 3: Securely Storing Credentials**
1 - In the Apps Script editor, go to File > Project properties > Script properties.
2 - Add new properties for DB_URL, DB_USER, and DB_PASS with the corresponding database URL, username, and password.

**Step 4: Script to Fetch Data and Write to Google Sheet**
Populates Google Sheet automatically every Sunday night with the latest data from the SQL query, providing a weekly overview of engagement statuses and ladder engagements

**Step 5: Scheduling the Script with a Trigger**
1 - Go back to the script editor and click on the clock icon (⏰) to open the triggers page.
2 - Click '+ Add Trigger' and configure it to run the fetchWeeklySnapshot function, time-driven, once a week, every Sunday, between 11 PM and midnight.

**NOTE:**
-- A correct count will require removing Salesforce IDs from Weekly Snapshot Eng/Eng Status (begin 4/14)that exists in Exclusions Google Sheet (https://docs.google.com/spreadsheets/d/1HVPN2BaMfGYESUmm0iyUCcEHzjwO9SucMlStAp6raFE/edit#gid=1050377494)

**NOTE:**
-- Google Sheets has a max of 10m cells (including empty cells) and script will fail if it runs over. For this Google Sheet, I deleted all columns to the right of the last column. Script includes instructions to count the number of cells in the Google Sheet

