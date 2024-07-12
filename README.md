# Advanced IP Address Ping Script

This PowerShell script automates the process of pinging multiple IP addresses, each in a new command prompt window, and logs the results to individual files.

## Introduction

This script is designed to help network administrators and IT professionals easily ping a list of IP addresses. Each IP address is pinged in a separate command prompt window, allowing for continuous monitoring of multiple hosts simultaneously. The results of each ping session are logged to individual text files.

## How It Works

The script defines a list of IP addresses to ping. It then uses a function to open a new command prompt window for each IP address and execute a continuous ping (`ping -t`). The output of each ping session is logged to a separate file named `PingLog_<IP>.txt`, where `<IP>` is the respective IP address.

## Features

- Pings multiple IP addresses concurrently.
- Opens a new command prompt window for each IP address.
- Continuous pinging for real-time monitoring.
- Logs results of each ping session to individual files.

## Dependencies

- PowerShell

## Getting Started

1. **Edit the Script:**
   - Open the script file (`ping_script.ps1`) in a text editor.
   - Modify the list of IP addresses to your desired IP addresses.
   - Save the script file.

2. **Run the Script:**
   - Open PowerShell.
   - Navigate to the directory where the script file is located using the `cd` command:
     ```powershell
     cd path\to\your\script\directory
     ```
   - Execute the script using the following command:
     ```powershell
     .\ping_script.ps1
     ```

3. **Monitor the Pings:**
   - Each IP address in the list will be pinged in a new command prompt window.
   - The results of each ping session will be logged to a file named `PingLog_<IP>.txt` in the script's directory.

## Script

```powershell
#---------------------------------------------------------------------------------------#
# Title:          Advanced IP Address Ping Script                                       #
# Description:    Easily ping a list of IP addresses and log results to files           #
# Author:         Anthony Constant                                                      #
#---------------------------------------------------------------------------------------#

# List of IP addresses to ping
$ipAddresses = @(
    "10.10.10.10",
    "10.10.20.10",
    "10.10.30.10",
    "10.10.20.100"       
)

# Function to open a new command prompt window and ping an IP address, logging the result to a file
function Ping-IP {
    param (
        [string]$ip
    )
    $logFile = "PingLog_$ip.txt"
    $script = "powershell -NoExit -Command `"ping $ip -t | Tee-Object -FilePath $logFile`""
    Start-Process "cmd.exe" -ArgumentList "/c start cmd.exe /k $script"
}

# Loop through the list of IP addresses and ping each one in a new command prompt window
foreach ($ip in $ipAddresses) {
    Ping-IP -ip $ip
}

Write-Host "Ping commands executed in new command prompt windows."
