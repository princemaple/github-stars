---
project: Microsoft-Activation-Scripts
stars: 166599
description: Open-source Windows and Office activator featuring HWID, Ohook, TSforge, and Online KMS activation methods, along with advanced troubleshooting.
url: https://github.com/massgravel/Microsoft-Activation-Scripts
---

Microsoft Activation Scripts (MAS)
==================================

Open-source Windows and Office activator featuring HWID, Ohook, TSforge, and Online KMS activation methods, along with advanced troubleshooting.

* * *

How to Activate Windows / Office / Extended Security Updates (ESU)?
-------------------------------------------------------------------

### Method 1 - PowerShell ❤️

1.  Click the **Start Menu**, type `PowerShell`, and open it.
    
2.  Copy and paste the code below and press **Enter.**
    
    -   For **Windows 8.1, 10 and 11**:
        
        ```
        irm https://get.activated.win | iex
        ```
        
        If the above is blocked (by ISP/DNS), try this (needs updated Windows 10 or 11):
        
        ```
        iex (curl.exe -s --doh-url https://1.1.1.1/dns-query https://get.activated.win | Out-String)
        ```
        
    -   **Script not launching? Use the below-listed Method 2.**
3.  In the menu that appears, type the number corresponding to one of the **Green** options.
    

* * *

### Method 2 - Traditional (Windows Vista and later)

1.  Download the script:
    -   **MAS\_AIO.cmd** (Direct script)
    -   **MAS\_AIO.zip** (If the direct script is blocked by your browser)
2.  Run the `MAS_AIO.cmd` file.
3.  In the menu that appears, type the number corresponding to one of the **Green** options.

* * *

Tip

-   Some ISPs/DNS providers block access to our domains. You can bypass this by enabling DNS-over-HTTPS (DoH) in your browser.
-   **Having trouble**? Visit our troubleshooting page or raise an issue on GitHub.

Note

-   The `irm` command in PowerShell downloads a script from a specified URL, and the `iex` command executes it.
-   Always double-check the URL before executing the command and verify the source is trustworthy when manually downloading files.
-   Be cautious of third parties spreading malware disguised as MAS by altering the URL in the PowerShell command.

* * *

### Homepage - https://massgrave.dev/

* * *

Latest Version: 3.10  
Release date: 28-Jan-2026
