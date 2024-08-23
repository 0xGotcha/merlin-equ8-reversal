# Malware Analysis Report: Merlin-Equ8 Reversal (-NoMerlin)

## 1. Executive Summary

This report provides a comprehensive analysis of the **Merlin-Equ8** sample and is not FULLY completed. The analysis covers its identified functionalities, key indicators of compromise (IoCs), and technical insights into the software's behavior. The report focuses on the malware's capabilities related to anti-cheat mechanisms and system information gathering.

## 1. Bottom Line Up Front - Does a intrusive malware anticheat work?

![image](https://github.com/user-attachments/assets/8843058a-e246-4ce0-8596-906958486752)


## 2. Overview

- **Sample Name:** Merlin-Equ8
- **Category:** Anti-Cheat Tool
- **Target Platform:** Windows
- **Date Analyzed:** 8/23/2024
- **Analyst:** Gotcha/sircapsalot

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

- **File Names:**
    - anticheat.x64.redkard.exe
    - client.x64.redkard.dll
    - redkard.sys
- **Hashes**
    -  DE44BE17C2DF928630D6542E6F43BB24D1894C6DD7154DEE4636217F2ADF1B0F
    -  3A2BC6BE1589DA3B28538886C86C732D2F34D7147A6DA3625642C6EAD847F81A
    -  9F7EA0C3EFBDEF23539A50689025A58240DD77AF4265EDF53339722BB91A8DE2

## 7. Conclusion and Recommendations

The **Merlin-Equ8** sample demonstrates a typical anti-cheat mechanism used in gaming environments. Its primary focus is on detecting cheat software and uniquely identifying systems through hardware signatures. While this is common in anti-cheat software, organizations must be cautious about data collection and potential privacy concerns.

### Recommendations:

- Monitor for the identified IoCs.
- Regularly update endpoint protection software.
- Conduct frequent system integrity checks.

---

# Fair Use End User License Agreement (EULA) for Merlin-Malware

**Effective Date:** 8/23/2024



This End User License Agreement (the "Agreement") governs your access to and use of the [malware analysis and research] (the "Content") published by [Your Name/Your Organization] (the "Publisher"). By accessing or using the Content, you agree to the terms and conditions outlined in this Agreement.

## 1. Purpose of the Content

The Content has been published with the purpose of:

1. Exposing, documenting, and analyzing malware found in public software for the **public interest**.
2. Informing the public of **security vulnerabilities**, **malicious behavior**, and **illegal activities** within the analyzed software.
3. Providing educational and research resources for security professionals, researchers, and the general public to better understand potential risks.

## 2. Fair Use and Legal Protections

This publication is fully protected under the **fair use** provisions of **U.S. copyright law** (17 U.S.C. § 107) and equivalent international laws. The Publisher has reverse-engineered and analyzed the software for the explicit purpose of exposing **malware** and **security vulnerabilities**, which are considered matters of public interest. As such, the following factors strongly support the classification of this work as fair use:

- **Transformative Use:** The Publisher's use of the original software is strictly for reverse-engineering and analysis purposes, to expose malicious activity, which is entirely distinct from the software's intended purpose.
- **Public Interest and Education:** The Content is intended to protect and inform the public about the dangers of the malware. It is also meant to educate security professionals and researchers on the nature of the malicious activity.
- **Minimal Use:** Only the portions of the software necessary to demonstrate the malware's behavior and document its harmful effects have been used.
- **No Harm to Market:** The Publisher’s use of the software does not interfere with the legitimate market value of the original work, as it is solely focused on its malicious components.

## 3. Whistleblower Protections

The Publisher discloses the presence of malware in publicly available software in good faith, in accordance with **whistleblower protections** granted under various U.S. and international laws, including but not limited to:

- **Whistleblower Protection Act** (5 U.S.C. § 2302): This law protects individuals who disclose illegal, unethical, or harmful behavior, including the presence of malware in public software.
- **Digital Millennium Copyright Act (DMCA) Exemption for Security Research**: The Publisher's actions fall under the **security research exemption** of the DMCA, as codified under **37 C.F.R. § 201.40** (Title 37: Patents, Trademarks, and Copyrights). This exemption allows security researchers to bypass digital rights management (DRM) and other technical protections when exposing vulnerabilities, such as malware, for public safety.

### 3.1 DMCA Security Research Exemption

The **DMCA Section 1201 Security Research Exemption** permits the circumvention of technological protection measures (TPMs) for the purposes of **good-faith security research**. The exemption was issued by the **Librarian of Congress** in 2018 and remains in effect under the following conditions:

- **Good Faith**: The research must be conducted in good faith for purposes of improving the security or safety of a computer, network, or device.
- **Lawful Acquisition**: The researcher must have lawfully acquired the software or device being examined.
- **Controlled Environment**: The research must be conducted in a controlled environment, ensuring that it does not harm others or the public at large.
- **Compliance with Other Laws**: The research must comply with applicable laws, including those related to computer hacking and privacy.

This exemption enables the Publisher to reverse-engineer and analyze the software for security purposes, consistent with public safety interests. For more details, please refer to the full text of the exemption in the **Library of Congress Rulemaking on Exemptions to Section 1201**, found [here](https://www.copyright.gov/1201/).

## 4. False DMCA Takedown Notices and Legal Action

This Content is protected under **fair use**, **whistleblower laws**, and the **DMCA Security Research Exemption**. Any party attempting to file a **false DMCA takedown notice** against this publication will face immediate legal action.

### 4.1 Liability for Misrepresentation (DMCA Section 512(f))

Under **17 U.S.C. § 512(f)**, any individual or entity that knowingly submits a **false DMCA takedown notice** by misrepresenting that the Content is infringing when it is clearly not will be held liable for damages, including the Publisher’s costs and attorney’s fees. The Publisher is prepared to pursue **all available legal remedies** against any party who attempts to suppress this research through improper use of the DMCA.

Should you submit a false DMCA takedown notice, the following penalties may apply:

- **Liability for Damages:** You may be held liable for any damages resulting from the disruption of the Publisher's work, including loss of income, harm to public education initiatives, and reputational harm caused by the improper takedown request.
- **Attorney’s Fees and Court Costs:** The Publisher will seek full recovery of all legal expenses related to defending the Content, including court costs and attorney’s fees.
- **Perjury and Legal Sanctions:** Filing a false DMCA takedown notice constitutes **perjury** under U.S. law. This can result in criminal charges, fines, and other legal penalties.

### 4.2 Legal Intent to Pursue Action

The Publisher hereby asserts the legal right to defend this publication and will not hesitate to take **legal action** against any party submitting a false DMCA takedown notice. This includes but is not limited to filing counter-notifications, seeking injunctions, and pursuing full damages in court.

The Publisher is protected by legal precedents, including **Lenz v. Universal Music Corp.**, which established that copyright holders must consider **fair use** before submitting DMCA takedown notices. Failure to respect these protections will result in aggressive legal recourse.

## 5. No Infringement Intended

The Publisher asserts that the Content is not intended to infringe upon any copyright or intellectual property rights. The analysis, documentation, and reverse-engineering contained in the Content are intended solely for **research, educational purposes**, and **public safety**. 

If you believe that any aspect of this Content infringes upon your rights, you may contact the Publisher at [Your Contact Information] to resolve the matter. However, the Publisher maintains that this Content is fully protected under **fair use**, **whistleblower laws**, and the **DMCA Security Research Exemption**.

## 6. Disclaimer of Liability

The Publisher is not responsible for any consequences that may arise from third parties who modify or misuse the Content. The reverse-engineering and malware documentation provided are for educational and security purposes only and are delivered "as is." The Publisher is not liable for any damages caused by the distribution of malware or modifications to the analyzed software by third parties.

## 7. Reporting Misuse or Errors

If you discover any inaccuracies in the documentation or believe there has been misuse of the Content, please contact the Publisher at [Your Contact Information] for a prompt review and correction.

## 8. Governing Law

This Agreement and all legal matters related to it shall be governed by and construed in accordance with the laws of [Insert Your Country/State]. Any legal disputes arising from this Agreement will be adjudicated in the courts of [Insert Country/State].

## 9. Amendments

The Publisher reserves the right to amend this Agreement at any time. If amendments are made, an updated version of this Agreement will be published at [Insert URL].

---

**By accessing and using the Content, you acknowledge that you have read, understood, and agreed to the terms of this EULA.**
