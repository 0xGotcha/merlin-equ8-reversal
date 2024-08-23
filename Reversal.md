# Malware Analysis Report: Merlin-Equ8 Reversal

## 1. Executive Summary

This report provides a comprehensive analysis of the **Merlin-Equ8** sample. The analysis covers the identified functionalities, key indicators of compromise, and technical insights into the malware’s behavior. The report focuses on the malware's capabilities related to anti-cheat mechanisms and information gathering on host systems.

## 2. Overview

- **Sample Name:** Merlin-Equ8
- **Category:** Anti-Cheat Tool
- **Target Platform:** Windows
- **Date Analyzed:** [Date]
- **Analyst:** [Your Name]

The purpose of this analysis is to reverse-engineer the provided sample to understand its key functionalities and potential risks.

## 3. Analysis Environment

- **Tools Used:** IDA Pro, Ghidra, x64dbg
- **System Configuration:** Windows 10 x64, Intel i7, 16 GB RAM
- **Virtualization:** Yes (VMware)

## 4. Capabilities and Functionalities

### 4.1 String Checks for Cheat Tools

One of the primary features of the Merlin-Equ8 sample is its ability to detect known cheat tool strings. The malware scans the host system for specific strings related to common cheat software used in gaming environments.

![String Check](https://github.com/user-attachments/assets/5a64d1fb-fd9b-4481-9037-eb513239c017)

**Description:**  
The malware contains hardcoded strings commonly associated with cheat tools. Upon execution, it compares these strings against running processes and loaded modules to detect the presence of cheating software.

**Impact:**  
The detection of these strings may trigger actions such as system shutdown, player bans, or log entries to the server, indicating a cheating attempt.

### 4.2 Gathers Hard Disk Information

The sample also gathers detailed information about the hard disk. This includes collecting serial numbers, manufacturer details, and partition information.

![Hard Disk Information](https://github.com/user-attachments/assets/e85eac01-f9bd-4338-95ad-3afe9f5a9005)

**Description:**  
The malware queries the system's hard disk using APIs to collect identifying information. This data may be used for generating hardware-based identifiers, which can be used to uniquely identify and track a system, or to prevent duplicate account creation on the same device.

**Impact:**  
The hard disk information could be used in anti-cheat mechanisms, ensuring that even if a user creates a new account, they are still identifiable via hardware signatures.

## 5. Technical Analysis

### 5.1 Code Overview

- **Language:** C++ (with CRT avoidance as per observed implementation style)
- **Obfuscation Techniques:** Minimal, primarily string obfuscation

### 5.2 Detailed Functional Flow

1. **Initialization:** The malware starts by gathering system details, including OS version, CPU architecture, and hard disk information.
2. **String Comparisons:** The malware iterates over a predefined list of cheat tool strings and searches them across running processes.
3. **Reporting:** If a match is found, the malware logs the details or communicates back to a remote server.

## 6. Indicators of Compromise (IoCs)

- **File Names:** [List of suspicious file names]
- **Registry Keys:** [List of any registry changes]
- **Network Connections:** [Details of any C2 server connections]

## 7. Conclusion and Recommendations

The **Merlin-Equ8** sample demonstrates a typical anti-cheat mechanism used in gaming environments. Its primary focus is on detecting cheat software and uniquely identifying systems through hardware signatures. While this is common in anti-cheat software, organizations must be cautious about data collection and potential privacy concerns.

### Recommendations:

- Monitor for the identified IoCs.
- Regularly update endpoint protection software.
- Conduct frequent system integrity checks.
