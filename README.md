# Server Health Monitor

A robust, continuous Windows Server monitoring script written in PowerShell that generates a beautiful, interactive, and premium HTML dashboard using Chart.js. The script gives you real-time insights into resource utilization, user impact, storage health, hardware stability, and application crashes.

## Features

- **Continuous Monitoring & History:** Runs silently in the background over a specified number of days, graphing resource trends to easily spot recurring performance bottlenecks.
- **Interactive HTML Report:** Premium UI with a dark-mode theme, live status badges, active alert highlights, and interactive hover-tooltips on trend charts.
- **Resource Utilization Tracking:** Captures CPU and memory usage at configurable intervals.
- **User Impact Analysis:** Groups processes by user to identify exactly who is consuming the most processing power and RAM on shared servers.
- **Application & Hardware Diagnositcs:** Discovers top CPU/RAM consuming applications, spots applications that are frequently crashing from the Event Logs, and flags failing hardware components (Disk/Network).
- **Intelligent Recommendations:** Evaluates the health of the system and outputs actionable warnings and critical alerts when thresholds are breached.
- **Active User Sessions:** Pulls metrics equivalent to `quser` to display who is currently logged into the server, along with idle times and session states.
- **Point-in-Time Snapshots:** Alternatively, use the `-RunOnce` switch to skip the background loop and take a one-time snapshot of the server's health.

## Example Report

A sample premium HTML report has been included in this repository. You can view it by downloading and opening `sample_report.html` in any web browser. 

The dashboard includes:
- Insights & Recommendations
- Resource Utilization Trend Charts (CPU & RAM)
- User Impact Bar Charts
- Logical Disk Summary & Hardware Errors
- Recent Critical Error Logs
- Top Consumer Apps & Active User Sessions

## Parameters

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `Days` | `[int]` | `7` | Number of days the script should continuously monitor the server. |
| `IntervalMinutes` | `[int]` | `15` | How often (in minutes) to take a snapshot for the HTML report. |
| `ExportPath` | `[string]`| `$env:USERPROFILE\Desktop\ServerHealthReport.html` | Save destination for the HTML file. |
| `RunOnce` | `[switch]`| `$false` | Instructs the script to take a single snapshot and exit immediately. |

## Usage Examples

**1. Default Run (7 Days, 15 Min Interval)**
```powershell
.\Monitor-ServerHealth.ps1
```

**2. Custom Continuous Run**
Monitors the server for 30 days, capturing data every 60 minutes, and saving the dashboard to a specific folder.
```powershell
.\Monitor-ServerHealth.ps1 -Days 30 -IntervalMinutes 60 -ExportPath "C:\Reports\MonthlyHealth.html"
```

**3. Point-in-time Snapshot**
Takes a single reading and immediately generates the report.
```powershell
.\Monitor-ServerHealth.ps1 -RunOnce -ExportPath "C:\Reports\Snapshot.html"
```

## Requirements
- PowerShell 5.1 or later.
- Must be run as an **Administrator** to fetch detailed Event Log data, User level process aggregation, and Active User details.
- Internet connectivity (Only on the machine opening the report) to load the Chart.js library via CDN. (Can be modified to use a local library).

## Security and Privacy
The script queries standard Windows WMI/CIM instances, Event Logs, and Processes. It relies purely on native tools within Windows. It does not phone home or transmit data securely anywhere; everything stays strictly on your server in the generated HTML report.

