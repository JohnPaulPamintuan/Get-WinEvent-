# Windows Security Log Analysis with Get-WinEvent
- The Get-WinEvent cmdlet is an indispensable tool in PowerShell for querying Windows Event logs en masse. The cmdlet provides us with the capability to retrieve different types of event logs, including classic Windows event logs like System and Application logs, logs generated by Windows Event Log technology, and Event Tracing for Windows (ETW) logs.

# Objective 
- To monitor and analyze Windows Event Logs, specifically focusing on security-related logs to identify potential security incidents and suspicious behavior. This project will demonstrate my ability to use PowerShell’s Get-WinEvent to filter and search logs for security detection.

# Requirements
- Windows machine with PowerShell 
- Basic knowledge of Windows Event IDs

# Using Get-WinEvent
- To quickly identify the available logs, we can leverage the -ListLog parameter in conjunction with the Get-WinEvent cmdlet. By specifying * as the parameter value, we retrieve all logs without applying any filtering criteria. This allows us to obtain a comprehensive list of logs and their associated properties. By executing the following command, we can retrieve the list of logs and display essential properties such as LogName, RecordCount, IsClassicLog, IsEnabled, LogMode, and LogType. The | character is a pipe operator. It is used to pass the output of one command (in this case, the Get-WinEvent command) to another command (in this case, the Select-Object command).

IMAGE 

  - This command provides us with valuable information about each log, including the name of the log, the number of records present, whether the log is in the classic .evt format or the newer .evtx format, its enabled status, the log mode (Circular, Retain, or AutoBackup), and the log type (Administrative, Analytical, Debug, or Operational).

- We can explore the event log providers associated with each log using the -ListProvider parameter. Event log providers serve as the sources of events within the logs. Executing the following command allows us to retrieve the list of providers and their respective linked logs.

IMAGE
  - This command provides us with an overview of the available providers and their associations with specific logs. It enables us to identify providers of interest for filtering purposes.

- Now, let's focus on retrieving specific event logs using the Get-WinEvent cmdlet. At its most basic, Get-WinEvent retrieves event logs from local or remote computers.
  - Retrieving events from the System log
 
  IMAGE

  - This example retrieves the first 50 events from the System log. It selects specific properties, including the event's creation time, ID, provider name, level display name, and message. This facilitates easier analysis and troubleshooting.
 
- Retrieving events from Microsoft-Windows-WinRM/Operational

IMAGE 
  - In this example, events are retrieved from the Microsoft-Windows-WinRM/Operational log. The command retrieves the first 30 events and selects relevant properties for display, including the event's creation time, ID, provider name, level display name, and message.

- To filter Windows event logs, we can use the -FilterHashtable parameter, which enables us to define specific conditions for the logs we want to retrieve.
IMAGE

  - The command above retrieves events with IDs 1 and 3 from the Microsoft-Windows-Sysmon/Operational event log, selects specific properties from those events, and displays them in a table format. Note: If we observe Sysmon event IDs 1 and 3 (related to "dangerous" or uncommon binaries) occurring within a short time frame, it could potentially indicate the presence of a process communicating with a Command and Control (C2) server.
 
- If we want the get event logs based on a date range (5/28/23 - 6/2/2023), this can be done as follows.
IMAGE


