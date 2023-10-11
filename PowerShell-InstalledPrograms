$outputFile = "$env:USERPROFILE\Installed_Applications.txt"

# Define the registry path to the uninstall information
$keyPath32Bit = "HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*"
$keyPath64Bit = "HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*"

# Get installed applications from both 32-bit and 64-bit registry paths
$apps32Bit = Get-ItemProperty -Path $keyPath32Bit |
    Where-Object { $_.DisplayName -ne $null } |
    Select-Object DisplayName, DisplayVersion, Publisher, InstallDate

$apps64Bit = Get-ItemProperty -Path $keyPath64Bit |
    Where-Object { $_.DisplayName -ne $null } |
    Select-Object DisplayName, DisplayVersion, Publisher, InstallDate

# Combine the results from both 32-bit and 64-bit registry paths
$allApps = $apps32Bit + $apps64Bit

# Sort the list by DisplayName
$allApps = $allApps | Sort-Object DisplayName

# Output the list to the specified text file
$allApps | Format-Table -AutoSize | Out-File -FilePath $outputFile -Encoding UTF8 -Force

Write-Host "List of installed applications has been saved to $outputFile"
