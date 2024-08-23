# Malware Analysis Report: Merlin-Equ8 Reversal

## 1. Executive Summary

This report provides a comprehensive analysis of the **Merlin-Equ8** sample. The analysis covers its identified functionalities, key indicators of compromise (IoCs), and technical insights into the software's behavior. The report focuses on the malware's capabilities related to anti-cheat mechanisms and system information gathering.

## 2. Overview

- **Sample Name:** Merlin-Equ8
- **Category:** Anti-Cheat Tool
- **Target Platform:** Windows
- **Date Analyzed:** 8/23/2024
- **Analyst:** Gotcha

This analysis aims to reverse-engineer the sample to uncover its key functionalities and potential risks.

## 3. Analysis Environment

- **Tools Used:** IDA Pro, Ghidra, x64dbg
- **System Configuration:** Windows 10 x64, Intel i7, 16 GB RAM
- **Virtualization:** Yes (VMware)

## 4. Capabilities and Functionalities

### 4.1 String Checks for Cheat Tools

One of the primary features of the Merlin-Equ8 sample is its ability to detect known cheat tool strings. The malware scans the host system for specific strings related to common cheat software used in gaming environments.

![String Check](https://github.com/user-attachments/assets/5a64d1fb-fd9b-4481-9037-eb513239c017)

**Description:**  
The malware contains hardcoded strings associated with known cheat tools. Upon execution, it compares these strings against running processes and loaded modules to detect the presence of cheating software.

**Impact:**  
The detection of these strings may trigger actions such as system shutdown, player bans, or log entries sent to a server, indicating a cheating attempt.

### 4.2 Gathers Hard Disk Information

The sample also gathers detailed information about the hard disk, such as serial numbers, manufacturer details, and partition information.

![Hard Disk Information](https://github.com/user-attachments/assets/e85eac01-f9bd-4338-95ad-3afe9f5a9005)

**Description:**  
The malware queries the system's hard disk using APIs to collect identifying information. This data may be used for generating hardware-based identifiers to uniquely track a system, preventing duplicate account creation on the same device.

**Impact:**  
The hard disk information could be used in anti-cheat mechanisms, ensuring that users cannot bypass bans by creating new accounts on the same hardware.

### 4.3 Process Enumeration

The malware enumerates all running processes to gather further insights into the system.

![Enumerate All Processes](https://github.com/user-attachments/assets/0c9856fb-c70f-4907-a7cb-08ac4935ef5c)

### 4.4 Gathers Registry Key Information and Checks

The malware examines specific registry keys for information and checks related to system configurations.

![Registry Information Check](https://github.com/user-attachments/assets/8a385f68-b261-48a3-8f2b-db887e048ecf)

### 4.5 Window Title Enumeration

The malware enumerates all window titles, likely to detect cheat tools by their window names.

![Window Title Enumeration](https://github.com/user-attachments/assets/ce353edf-28c3-46e1-ae21-3718e766d552)

### 4.6 Screenshots and Monitor Enumeration

The malware captures screenshots and enumerates monitor details to monitor the system's display environment.

![EnumMonitor](https://github.com/user-attachments/assets/f8d30354-a27f-4d58-8a92-88f0935309a2)

### 4.7 Trusted Status Reporting: Anti-Cheat or Malware?

The sample checks for whether the system is considered "trusted" and reports back accordingly.

![Trusted Status Reporting](https://github.com/user-attachments/assets/05da8a02-e9fe-431f-ab05-26b59f01a6dd)

### 4.8 Test Signing Mode Check

The malware checks if TestSigning mode is enabled to prevent the use of unsigned drivers.

![Test Signing Mode Check](https://github.com/user-attachments/assets/064367f7-7055-4816-8925-c2d028da11f0)

### 4.9 Obtaining UEFI Variables
![uefivariables](https://github.com/user-attachments/assets/5746c1e5-6168-44dc-b916-33111c069939)



## 5. Technical Analysis

### 5.1 Code Overview

- **Language:** C++ (with CRT avoidance based on observed implementation style)
- **Obfuscation Techniques:** Minimal, primarily string obfuscation

### 5.2 Detailed Functional Flow

1. **Initialization:** The malware starts by gathering system details, including OS version, CPU architecture, and hard disk information.
2. **String Comparisons:** It iterates over a predefined list of cheat tool strings and searches them across running processes.
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

---

# Fair Use End User License Agreement (EULA) for Merlin-Malware

**Effective Date:** 8/23/2024

## 1. Introduction

This End User License Agreement ("EULA") is a legal agreement between you and [Your Name or Organization] ("Licensor") regarding the use of the software code, documentation, and other content provided in the Merlin-Malware repository (the "Software"). By using or contributing to this Software, you agree to the terms of this EULA.

## 2. License Grant and Fair Use

Subject to the terms of this EULA, the Licensor grants you a limited, non-exclusive, non-transferable, and revocable license to use, modify, and distribute the Software under the principles of **Fair Use**, as outlined by copyright law and as explained in this agreement. This includes:

- **Educational Use:** You may use the Software for educational and research purposes.
- **Non-Commercial Use:** You may use the Software for personal or non-commercial projects.
- **Commentary and Criticism:** You may use parts of the Software to provide commentary, criticism, or analysis.

## 3. Prohibited Uses

The following actions are prohibited:

- **Infringing Use:** Any use that violates copyright law or is intended to bypass fair use protections.
- **Commercial Exploitation:** Selling, sublicensing, or distributing the Software in a way that constitutes a direct commercial product is not allowed without explicit permission from the Licensor.

## 4. Copyright and Attribution

The Software may contain copyrighted material, trademarks, or other proprietary information. Any content used under fair use must be attributed to its original author. The Licensor does not claim ownership over third-party content that is integrated into the Software.

## 5. No Warranties

The Software is provided "as is," without any warranties of any kind, either express or implied, including, but not limited to, implied warranties of merchantability, fitness for a particular purpose, or non-infringement.

## 6. DMCA and Legal Compliance

While this EULA is designed to protect fair use rights, the Licensor acknowledges that all content on GitHub is subject to DMCA takedown procedures. If you believe that content in this repository violates your rights, please contact us directly before filing a DMCA notice.

## 7. Limitation of Liability

To the maximum extent permitted by law, in no event shall the Licensor be liable for any damages arising out of the use of the Software, whether in an action of contract, negligence, or other tortious action.

## 8. Modifications to the EULA

The Licensor reserves the right to modify this EULA at any time. Any updates will be posted to this repository, and continued use of the Software constitutes acceptance of any modified terms.

## 9. Contact Information

If you have any questions or concerns regarding this EULA or the Software, please contact us at [Your Email Address].
