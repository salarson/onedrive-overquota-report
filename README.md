# Get-ODBOverQuotaUsers

A PowerShell script for identifying OneDrive for Business users who are over their **expected** storage quota based on their assigned license tier, with special handling for EDU A1 enforcement.

The script uses **Microsoft Graph exclusively** — no SharePoint Online Management Shell, no PnP, no ImportExcel, no third-party modules. Works on Windows PowerShell 5.1+ and PowerShell 7+, on commercial, GCC High, DoD, and 21Vianet (China) tenants.

---

## Why this script exists

OneDrive sites are provisioned with a default storage quota based on tenant settings, but the *expected* quota varies by license tier. EDU A1 users, for example, are entitled to 100 GB — but if they were provisioned before A1 enforcement kicked in, they may have a 1 TB or 5 TB allocation and be using more than 100 GB today.

This script answers a single question for an admin:

> **Which OneDrive sites are storing more data than the owner's license tier entitles them to?**

It outputs a console summary plus an optional CSV containing **every** evaluated site with an `OverQuota` True/False column so admins can filter/pivot in Excel.

---

## Quick start

```powershell
# First run on a new machine: install required Graph modules
.\Get-ODBOverQuotaUsers.ps1 -InstallPrerequisites

# Default run — FastScan, console output only
.\Get-ODBOverQuotaUsers.ps1

# Default run with CSV export (recommended)
.\Get-ODBOverQuotaUsers.ps1 -ExportPath "C:\Reports\OneDriveQuota.csv"