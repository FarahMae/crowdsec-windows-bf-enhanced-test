# CrowdSec Windows Brute-force Enhanced Detection Test

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Platform](https://img.shields.io/badge/Platform-Windows-blue)
![Log](https://img.shields.io/badge/Log-Windows%20Syslog-yellow)

This repository provides a custom parser test for CrowdSec to verify enhanced detection of failed Windows login attempts. It focuses specifically on the accurate extraction of the **target username**, in response to [CrowdSec Hub Issue #1235](https://github.com/crowdsecurity/hub/issues/1235).

## Overview

Windows authentication logs often contain valuable information about failed login attempts. This test ensures that CrowdSec's parser correctly identifies and extracts the username of the account being targeted in these logs, which is essential for detecting brute-force attacks.

## Objectives

- Simulate a Windows failed logon event via syslog.
- Confirm that the CrowdSec parser can extract:
  - Target `Account Name` (username)
  - `Workstation Name`
  - Log timestamp
  - Program source (e.g., `Microsoft-Windows-Security-Auditing`)

## Files Included

windows-bf-enhanced/ ├── config.yaml # Specifies which parsers to test ├── parser.assert # Validates parser output fields ├── scenario.assert # Ensures no scenarios are incorrectly triggered └── windows-bf-enhanced.log # Simulated Windows Security log (failed logon)

## Sample Log Used

Feb 15 08:42:30 WIN-HOSTNAME Microsoft-Windows-Security-Auditing: An account failed to log on. Subject: Security ID: NULL SID Logon ID: 0x0 Account Name: - Account Domain: - Logon Type: 3 Account For Which Logon Failed: Security ID: NULL SID Account Name: testuser Workstation Name: WIN-HOSTNAME Failure Information: Failure Reason: Unknown user name or bad password Status: 0xc000006d Sub Status: 0xc000006a

## How to Use

> ✅ Prerequisites: CrowdSec v1.6+ installed and the `cscli` tool available.

1. **Clone the CrowdSec Hub repository**

   git clone https://github.com/crowdsecurity/hub
   cd hub
Copy this test into your .tests folder

cp -r /path/to/crowdsec-windows-bf-enhanced-test/windows-bf-enhanced .tests/

Run the test:

sudo cscli hubtest run windows-bf-enhanced

Expected Output:

All tests passed, use --report-success for more details.
This means the log was successfully parsed, and no false alerts were triggered.

Technical Details

Test Type: syslog

Parsers Tested:

crowdsecurity/syslog-logs

crowdsecurity/dateparse-enrich

Expected Behavior: Parser extracts all relevant fields correctly; no scenario (alert) is expected to trigger with just a single log.

Related Issue
This test was built to support:
Issue #1235 - Should catch windows BF target username

About the Author
Farah Mae Sumajit
Cybersecurity Enthusiast | SOC & Threat Detection Projects
📍 Based in Israel | 🇵🇭 Filipino
🔗 LinkedIn Profile
📫 Contact: sumajitfarahmae5@gmail.com

License
This project is licensed under the MIT License.
