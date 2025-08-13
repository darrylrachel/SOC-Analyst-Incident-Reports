# SOC INCIDENT CARD – Passwd Found in Requested URL - Possible LFI Attack

**Date/Time:** Mar 01, 2022, 10:10AM  
**Event ID:** 120  
**Location:** WebServer1006 | 172.16.17[.]13   
**Severity:** High

## 1. Summary
Event 120 was triggered by a URL contains passwd rule that was blocked by the firewall

---

## 2. Attack Indicators
| Field              | Value                                                                  |
|--------------------|------------------------------------------------------------------------|
| **Detection Rule** | SOC170 Passwd Found in Requested URL - Possible LFI Attack             |
| **Attack Type**    | LFI Web Application Attack                                             |
| **Device Action**  | Allowed            			                                          |
| **HTTP Method**    | GET                                                                    |
| **Response Code**  | 500                                                                    |

---

## 3. Observed Activity
Request URL: hxxps://172.16.17[.]13/?file=../../../../etc/passwd

---

## 4. Source Information
- **IP:** 106.55.45[.]162  
- **Geo:** Haidian District Beijing, China  
- **Owner/ISP:** Tencent cloud computing (Beijing) Co., Ltd. (Data Center/Web Hosting/Transit)  
- **Reputation:** Known malicious  

---

## 5. Analysis
- **What it is:** Local File Inclusion (LFI) attack. An attacker exploits a vulnerability in a web application to access, view, and potentially include local files on the web server's file system. This can be done by manipulating file paths within the application, often through user-supplied input like URL parameters or form data. Successful exploitation can lead to information disclosure, code execution, or even complete system compromise. 
- **Why it matters:** Attackers can use ".." sequences (or similar techniques) to navigate up the directory structure and access files outside the intended directory.   
- **Evidence:**
		RAW LOG
			Request URL: hxxps://172.16.17[.]13/?file=../../../../etc/passwd
			User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)
			Request Method: GET
			Device Action: Permitted
			HTTP Response Size:: 0
			HTTP Response Status: 500 (Internal Server Error)
- **Impact if exploited:** Attackers can gain access to sensitive files like configuration files, database credentials, or system logs. 

---

## 6. Recommended Actions
- Thoroughly validate all user-supplied inputs to prevent directory traversal attempts.  
- Use a whitelist of allowed file paths or IDs, and reject any input that doesn't match.  
- Remove or encode potentially malicious characters from user input.  
- Run web applications with the least necessary privileges to minimize the potential impact of an attack.  

---

**Final Verdict:** True Positive, attack not successful
