# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file 
2. PDF convertor access for our unit
3. PDF convertor having access to report file 
4. PDF convertor hacing access to PDF storage data
5. PDF storing status expected from server
6. Notification client access for our unit
7. Access for mail client to PDF storing database (in case if PDF to be mailed)
8. Notification client takes care of address/number check and does proper alert/ error reaction
9. The data in csv file holds date,time and telemetrics data stored (to record trends)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|----------------------------------
Battery Data-accuracy       | No            | We do not test the accuracy of data 
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No 	          | Converter is another client which reads the analysis data stored as a text file adn converts the same
Counting the breaches       | Yes 	        | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | No	          | Notification alert via mail is done by mail client
PDF file storage            | Yes           | Storage status verified by software adn notification triggered if success or failed

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Find if the inputs are valid from CSV file 
2. Find minimum and maximum from a csv containing positive and negative readings
3. Find breach count from the readings available in CSV file
4. Find the trend of breaches from the readings available in CSV file
5. Record min/max/brach count/trend data from csv file
6. Convert recorded data to PDF when a week is over
6. Notification alert of PDF storage / conversion status (alerts if storing / conversion of PDF fails)
7. Write "Invalid input" to the PDF when the csv doesn't contain expected data


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input         | Output                      | Faked/mocked part
|--------------------------|---------------|-----------------------------|---
Read input from server     | csv file      | internal data-structure     | Fake the server store
Validate input             | csv data      | valid / invalid             | None - it's a pure function
Notify report availability | Report details| notification status         | Mock the notification client service
Report inaccessible server | server address| Access response             | Mock the server with dynamic storage and access responses
Find minimum and maximum   | csv data      | Min/ Max value              | None - it's a pure function
Detect trend               | csv data      | trend value                 | None - it's a pure function
Write to PDF               | Recorded data | PDF conversion status       | Mock PDF convertor function


* Here report details include report storage path, report archival status
