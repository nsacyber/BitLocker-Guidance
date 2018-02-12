# BitLocker Compliance
The BitLocker [audit file](./BitLocker.audit) can be used to verify implementation of the BitLocker settings. The Nessus audit file provides an automated way of verifying as many checks as possible. DoD components can acquire Nessus via the [ACAS](http://www.disa.mil/cybersecurity/network-defense/acas) program.

## Running Compliance Checks

There are two ways you can check compliance with the provided audit files:
1. Use Nessus
1. Use the provided Compliance PowerShell script (Nessus not required)

### Domain Scan with Nessus

1. Download the above .audit files
1. For each audit file make a new **Policy Compliance Auditing** scan
1. Configure the correct set of machines to scan and provide the correct credentials for the scan
1. On the **Compliance** tab, select **Windows** and then select **Upload a custom Windows audit file**
1. Run the scan and review the results

A paid version of Nessus Professional or Nessus Manager must be used in order to use .audit files with Nessus. The .audit files have been tested and work on Nessus Professional version 7.0. They may work on older versions as well but they have not been tested. Alternatively, you can use the provided PowerShell script to locally scan a single system.

### Standalone Scan with PowerShell

The **Test-Compliance** command in the [Compliance PowerShell module](./Scripts/) can be used to verify compliance against using any of the above listed .audit files. This PowerShell script makes it simple to scan a single standalone system and verify a configuration has been applied to a system in a non-domain context. Note that Nessus is not required to be installed on the system that is being checked with the script. The following instructions can be used to execute a compliance check locally.

1. Open a PowerShell prompt as an administrator
1. Change directory to the Compliance\Scripts directory (e.g. **cd BitLocker-Guidance\Compliance\Scripts**)
1. Import the [Compliance PowerShell module](./Scripts/) to load the code into the PowerShell session: `Import-Module -Name .\Secure-Host-Baseline\Compliance\Scripts\Compliance.psm1`
1. ```Test-Compliance -Path '.\BitLocker Guidance\Compliance\BitLocker.audit'``` and press Enter twice
  
   
The Compliance script supports a **-Verbose** option that show details for checks that fail. Without the verbose option a simple pass/fail is displayed for each compliance check as shown in the image below. 

Verbose example:
```
Test-Compliance -Path '..\..\BitLocker\Compliance\BitLocker.audit' -Verbose
```

Verbose example with capturing the output into a file:

```
Test-Compliance -Path '..\..\BitLocker\Compliance\BitLocker.audit' -Verbose .\*>BitLockerComplianceReport.txt
```

After capturing the output into a file, the failed  checks can be filtered using this PowerShell command:

```
Select-String -Path .\BitLockerComplianceReport.txt -Pattern 'FAILED'
```

## Links
* [Nessus Compliance Checks Reference (PDF)](https://docs.tenable.com/nessus/compliancechecksreference/Content/Resources/PDF/NessusComplianceChecksReference.pdf)
* [Nessus Compliance Checks Reference (HTML)](https://docs.tenable.com/nessus/compliancechecksreference/Content/ComplianceCheckTypes.htm)
* [Nessus Compliance Checks Overview (PDF)](https://support.tenable.com/support-center/nessus_compliance_checks.pdf)



