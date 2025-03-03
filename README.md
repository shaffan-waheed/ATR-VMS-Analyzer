# ATR - VMS Analyzer

![ATR - VMS Analyzer Splash Screen](atr_propeller.png)  
*Developed by Shaffan Waheed for the ATR Community*

[![Python Version](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)  
[![License](https://img.shields.io/badge/license-GPL--3.0-green.svg)](LICENSE)

## Overview

Welcome to **ATR - VMS Analyzer**, a tool designed to analyze propeller vibration data from ATR aircraft MPC reports. This software automatically processes `REPORT26` files stored locally on your PC, providing vibration trend analysis for propeller balancing and maintenance purposes. It is built for ATR aircraft equipped with the Vibration Monitoring System (VMS).

On ATR aircraft with VMS installed, propeller balancing reports are generated based on VMCU outputs and stored on the MPC PCMCIA card as `Report 26`. The software supports two types of measurements:

- **Automatic Vibration Monitoring**: No operator action required. VMS monitors vibration levels in cruise and calculates balancing weight solutions if needed. Reports are created if one of the following conditions are   met:
  - Every 50 flights on flight transition from 08 (Landing Roll) to 09 (Taxi-in)
  - When on flight transition from 08 to 09 the vibration amplitude parameter is greater than IPS threshold.
    **OR** 
  - Every flight if vibration exceeds 1 IPS, until corrective action is taken, or when thresholds set in the MCDU VMS menu are exceeded.
 
    Note: The frequency of automatic report generation can be adjusted from MCDU>ACMS>VMS>UPDATE AUTO REPORT FREQ
- **Manual Measurement**: Reports are generated whenever a manual measurement is commanded via MCDU.


## Prerequisites

This software is compatible with:

- **Aircraft Modifications**:
  - SB ATR72-61-1031 (Mod No's: 07736, 07835)
  - SB ATR42-61-0046 (Mod No's: 07736, 07835)
- **Operating System**: Windows-based PCs.
- **Data Requirements**:
  - All contents of the MPC card from the aircraft(s) must be saved in one directory on your PC.
  - Note: The software can process an entire hard disk if needed.

## Installation

### Running from Source
- Clone the repository from GitHub and navigate to the project directory.
- Ensure you have Python 3.8+ installed, then install the required packages using the provided `requirements.txt`.
- Create a `requirements.txt` file with the necessary dependencies: PyQt6 (version 6.4.0), pandas (version 1.5.0), numpy (version 1.23.0), and matplotlib (version 3.6.0).
- Run the application using Python with the main script (e.g., `main.py`).

### Running the Executable
- Download the latest release `ATR_VMS_Analyzer_v1.1.exe` file from the [Releases](https://github.com/shaffan-waheed/atr-vms-analyzer/releases) section of this repository.
- Place the `.exe` file in a directory of your choice on your Windows PC.
- Double-click the `ATR - VMS Analyzer v1.0.exe` file to launch the application.
- **Note on Windows Warnings**: Since this executable is not digitally signed, Windows may display a "Windows Defender SmartScreen" warning stating "Windows protected your PC" or "The publisher could not be verified." To proceed:
  - Click "More info" (if available) on the warning dialog.
  - Select "Run anyway" to bypass the warning and launch the application.
  - This warning occurs because the executable lacks a code-signing certificate, which is common for independent open-source projects but does not indicate a security threat.

## Getting Started

1. **Select Folder**:
   Click the "Select Folder" button at the top to choose the directory containing your MPC folders. The software will automatically process all valid `REPORT26` files, populate the aircraft and flight phase dropdowns, and set the date range based on the data.

## Using the Interface

- **Aircraft**:
  Select the aircraft (e.g., `8Q-XXX`) from the "Aircraft" dropdown to filter data for that aircraft. Note: Invalid aircraft registrations such as `000001` or `000003` are detected when aircraft registration is not updated properly on the aircraft MPC/MCDU.
- **Flight Phase**:
  Choose "All Phases" or a specific flight phase (e.g., "01: Pre-Flight") from the "Flight Phase" dropdown to filter data by phase. Configured Flight Phases:
  - 01: Pre-Flight
  - 02: Taxi-Out
  - 03: Take off Roll Initial
  - 04: Take off Roll Final
  - 05: Initial Climb
  - 06: Flight Phase (*TIP: Use this phase for propeller balancing purposes*)
  - 07: Final Approach
  - 08: Landing Roll
  - 09: Taxi In
  - 10: Post Flight
- **Date Range**:
  Adjust the "From Date" and "To Date" using the calendar popups to set the date range for the data. The start date defaults to the earliest date for the selected aircraft, and the end date defaults to the current date (e.g., 24-Feb-2025).
- **Generate Graph**:
  Click the "Generate Graph" button or modify any filter to automatically regenerate the graph, showing vibration trends for Propeller #1 (blue) and Propeller #2 (red), along with threshold lines. The line colors can be adjusted using the settings menu.

## Understanding the Graph

- **Graph Elements**:
  - **Propeller #1**: Blue line with circular markers.
  - **Propeller #2**: Red line with circular markers.
  - **User Threshold**: Green dashed line (default 0.1 IPS, adjustable via Settings > Threshold Settings).
  - **Aircraft Threshold**: Orange dashed step line, reflecting the actual threshold values detected in each report file.
- **Interactivity**:
  - Hover over data points to see IPS, balance recommendation, and phase details in a tooltip.
  - Click a data point to open a popup with detailed report information for that propeller, including weight configurations and an option to open the full report file.

## Menu Options

- **File > Export Graph**:
  Save the current graph as a PNG file, including all lines, labels, and the watermark.
- **Settings > Graph Colors**:
  Change the colors of Propeller #1, Propeller #2, User Threshold, and Aircraft Threshold lines using a color picker.
- **Settings > Threshold Settings**:
  Change the user threshold line (default is 0.1 IPS).
- **Help > Instructions**:
  View this user guide.
- **About > About**:
  Display information about the software and contact details for support.

## Additional Features

- **Log Area**:
  The log area at the bottom shows processing status, warnings, and errors for report files.

## Troubleshooting

- **Parsing Issues**:
  If reports fail to parse, check the log for warnings (e.g., invalid date formats or non-numeric thresholds). Ensure report files follow the expected format (e.g., `B2` line with date and aircraft, `C1` line with threshold, `D2`/`E2` for IPS values).
- **Support**:
  Report bugs and feature requests to [shaffan.waheed@gmail.com](mailto:shaffan.waheed@gmail.com).

## Contributing

Contributions are welcome! Please fork the repository, make your changes, and submit a pull request. Ensure your code follows the existing style and includes appropriate documentation.

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

---

*Thank you for using ATR - VMS Analyzer v1.0!*
