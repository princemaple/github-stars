---
project: Microsoft-Activation-Scripts
stars: 156181
description: Open-source Windows and Office activator featuring HWID, Ohook, TSforge, and Online KMS activation methods, along with advanced troubleshooting.
url: https://github.com/massgravel/Microsoft-Activation-Scripts
---

Microsoft Activation Scripts (MAS)
==================================

Open-source Windows and Office activator featuring HWID, Ohook, TSforge, and Online KMS activation methods, along with advanced troubleshooting.

* * *

How to Activate Windows / Office / Extended Updates (ESU)?
----------------------------------------------------------

### Method 1 - PowerShell ❤️

1.  **Open PowerShell**  
    Click the **Start Menu**, type `PowerShell`, then open it.
    
2.  **Copy and paste the code below, then press enter.**
    
    -   For **Windows 8, 10, 11**: 📌
        
        ```
        irm https://get.activated.win | iex
        ```
        
        If the above is blocked (by ISP/DNS), try this (needs updated Windows 10 or 11):
        
        ```
        iex (curl.exe -s --doh-url https://1.1.1.1/dns-query https://get.activated.win | Out-String)
        ```
        
    -   For **Windows 7** and later:
        
        ```
        iex ((New-Object Net.WebClient).DownloadString('https://get.activated.win'))
        ```
        
    -   **Script not launching❓Use the below-listed Method 2.**
3.  The activation menu will appear. **Choose the green-highlighted options** to activate Windows or Office.
    
4.  **Done!**
    

* * *

### Method 2 - Traditional (Windows Vista and later)

1.  Download the script: **MAS\_AIO.cmd** or the full ZIP.
2.  Run the file named `MAS_AIO.cmd`.
3.  You will see the activation options. Follow the on-screen instructions.
4.  That's all.

* * *

Tip

-   Some ISPs/DNS block access to our domains. You can bypass this by enabling DNS-over-HTTPS (DoH) in your browser.
-   **Having trouble**❓Visit our troubleshooting page or raise an issue on GitHub.

* * *

-   To activate additional products such as **Office for macOS, Visual Studio, RDS CALs, and Windows XP**, check here.
-   To run the scripts in unattended mode, check here.

* * *

Note

-   The IRM command in PowerShell downloads a script from a specified URL, and the IEX command executes it.
-   Always double-check the URL before executing the command and verify the source if manually downloading files.
-   Be cautious, as some spread malware disguised as MAS by using different URLs in the IRM command.

* * *

```
Latest Version: 3.8
Release date: 11-Nov-2025
```

### Troubleshooting / Help

### Download Original Windows & Office

### Homepage - https://massgrave.dev/

* * *

Made with Love ❤️
