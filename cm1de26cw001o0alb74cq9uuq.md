---
title: "Automating MSI Uninstalls with PowerShell for .NET MAUI Fix"
seoTitle: "Batch Uninstalling .NET SDKs Using PowerShell for .NET MAUI Fix"
seoDescription: "Learn how to automate the batch uninstallation of .NET SDKs using PowerShell."
datePublished: Sun Sep 22 2024 09:41:08 GMT+0000 (Coordinated Universal Time)
cuid: cm1de26cw001o0alb74cq9uuq
slug: automating-msi-uninstall
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726998555852/22ac1c91-cbf7-4dbd-88c3-194e48da27ba.png
tags: automation, powershell, troubleshooting, msi, net-maui, net-sdk

---

Recently, I found myself in a pickle trying to install .NET MAUI on my laptop, so I did a bit of searching and found out it was apparently a common issue.

### Problem: Can't locate .NET MAUI Workloads

According to [Microsoft's troubleshooting page](https://learn.microsoft.com/en-us/dotnet/maui/troubleshooting?view=net-maui-8.0), when dealing with the ‘Can’t locate the .NET MAUI workloads' problem:

1. **Uninstall the .NET MAUI workloads** through the CLI.
    
2. **Uninstall any .NET SDKs** in Control Panel.
    
3. **Uninstall the .NET MAUI workloads in Visual Studio.**
    

### Automating the Process with PowerShell

After taking the steps above, I realized there were still leftover SDKs on my machine.

These leftover SDKs can conflict with newer installations, especially when installing workloads like .NET MAUI. Running the following `reg query` command helps identify these 'hidden' SDKs that aren't visible in traditional uninstallation methods, allowing for a more thorough cleanup.

```plaintext
reg query HKLM\SOFTWARE\Microsoft\Windows\currentversion\uninstall\ -s -f manifest
```

Executing the command showed me this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726820124462/1612973b-d70f-4ff1-bdac-2c7ce03f9d77.png align="left")

Which meant I had to uninstall each of these 52 SDKs with the `msiexec` command below until the `reg query` command returned 0 matches.

```plaintext
msiexec /x {GUID} /q IGNOREDEPENDENCIES=ALL
```

After uninstalling about 11 SDKs, I realized this manual approach wasn’t exactly productive as it was time consuming and I spelt ‘DEPENDENCIES’ wrong a couple of times. So, I wrote a PowerShell script to automate it with the help of this [reddit ask](https://www.reddit.com/r/PowerShell/comments/c4rx1r/how_to_batch_uninstall_msi/) and ChatGPT. By automating the process, the repetitive task of uninstalling each GUID is done without error or wasted time.

Here’s the script that saved me minutes:

### PowerShell Script to Batch Uninstall MSI Files

```powershell
# Function to run the reg query and return the result
function Get-InstalledPrograms {
    # Run the reg query and return the output
    $output = & reg query HKLM\SOFTWARE\Microsoft\Windows\currentversion\uninstall\ -s -f manifest
    return $output
}

# Function to uninstall programs using msiexec
function Uninstall-Program {
    param (
        [string]$guid
    )
    # Uninstall using msiexec with the specific command and flags
    Write-Host "Uninstalling program with GUID: $guid"
    Start-Process "msiexec.exe" -ArgumentList "/x $guid /q IGNOREDEPENDENCIES=ALL" -Wait
    Write-Host "Uninstallation complete for GUID: $guid"
}

# Loop to keep running reg query until no results are returned
do {
    # Get the list of installed programs
    $installedPrograms = Get-InstalledPrograms

    # Define a list to store GUIDs for uninstallation
    $msiGuids = @()

    # Extract the GUIDs from the reg query output
    foreach ($line in $installedPrograms) {
        if ($line -match "({[A-Z0-9\-]+})") {
            $msiGuids += $matches[1]  # Extract the GUID from the match
        }
    }

    # If there are no GUIDs left, stop the loop
    if ($msiGuids.Count -eq 0) {
        Write-Host "No more programs to uninstall."
        break
    }

    # Loop through each extracted GUID and uninstall the program
    foreach ($guid in $msiGuids) {
        Uninstall-Program -guid $guid
    }

} while ($msiGuids.Count -gt 0)
```

### Steps to Use the Script:

1. **Run the PowerShell script**:
    
    * Save the script to a `.ps1` file.
        
    * Open PowerShell as Administrator.
        
    * Run the script: `.\your_script.ps1`.
        

This is where I ran into an error due to the **execution policy** in PowerShell, which controls the level of script execution allowed on your system. PowerShell execution policies act as a security mechanism to prevent malicious scripts from running on your system.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726821162886/c22ecee6-e697-4ac7-9edb-b6a52330f407.png align="center")

### Change the PowerShell Execution Policy (if needed)

I first checked the current execution policy by running this in PowerShell:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727149162641/3d8d868a-6c13-4af3-b4e7-99d11f714e47.png align="center")

By default, it is set to the 'Restricted' policy which blocks all scripts. I then changed the execution policy to `RemoteSigned` (allows you to run local scripts but still blocks scripts downloaded from the internet unless they are signed) using the following command in **PowerShell as Administrator**:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727148840532/ba551d98-50bc-45fd-a09a-0cf3fe248bdf.png align="center")

Then I ran the script again and this time….

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726821594205/78ec4d46-9c4c-4b58-b617-6a7c33a3eaf0.png align="center")

It worked!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726821688916/9f20bd56-0778-45a9-ad70-568b61f78b01.png align="center")

I was then finally able to reinstall .NET MAUI through Visual Studio (after uninstalling and reinstalling Visual Studio and Visual Studio Installer as a whole though 😅).

Note: I set my powershell execution policy back to restricted after running the script.

Thank you Microsoft Docs + ChatGPT + Reddit! (and sorry for the blurry screenshots).  
If you read this till the end, I hope you have learned something useful! 😊✨