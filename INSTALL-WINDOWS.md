# FortiCNAPP Agent Installation Guide for Windows

This guide provides step-by-step instructions for installing the FortiCNAPP agent on a Windows machine.

## Prerequisites

- A Windows machine running a supported version of Windows
- Administrator privileges on the machine
- Internet connectivity
- PowerShell (typically pre-installed on Windows)

## Getting the Installation URL

1. Log in to your FortiCNAPP console
2. Navigate to **Settings** > **Agent Tokens**
3. Click **Add New** > **Windows**
4. Click **Actions** > **Install**
5. Click **Copy URL** to copy the installation script URL

The URL will look like:
```
https://<account>.lacework.net/mgr/v1/download/<token>/install.ps1
```

## Installation

On the target Windows machine, follow these steps:

1. **Open PowerShell as Administrator**:
   - Click on the **Start** menu
   - Type `PowerShell`
   - Right-click on **Windows PowerShell** and select **Run as administrator**

2. **Download the Installation Script**:
   ```powershell
   Invoke-WebRequest -Uri "<INSTALLATION_URL>" -OutFile "install.ps1"
   ```

   Replace `<INSTALLATION_URL>` with the URL you copied from the FortiCNAPP console.

   **Example:**
   ```powershell
   Invoke-WebRequest -Uri "https://<account>.lacework.net/mgr/v1/download/<token>/install.ps1" -OutFile "install.ps1"
   ```

3. **Run the Installation Script**:
   ```powershell
   .\install.ps1
   ```

   If you encounter execution policy restrictions, you can temporarily bypass them by running:
   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force
   .\install.ps1
   ```

   After the installation, it's recommended to revert the execution policy:
   ```powershell
   Set-ExecutionPolicy Restricted -Scope Process -Force
   ```

**Complete Example:**
```powershell
Invoke-WebRequest -Uri "https://<account>.lacework.net/mgr/v1/download/<token>/install.ps1" -OutFile "install.ps1"
Set-ExecutionPolicy Bypass -Scope Process -Force
.\install.ps1
```

## Verification

After installation, verify that the agent is running:

1. Open **Run** by pressing `Win + R`
2. Type `services.msc` and press Enter
3. In the **Services** window, look for a service named **Lacework** or **FortiCNAPP Agent**
4. Ensure its status is **Running**

Alternatively, you can check the service status using PowerShell:

```powershell
Get-Service -Name "*lacework*"
```

## Configuration

The agent configuration file is typically located at:
```
C:\ProgramData\Lacework\config\config.json
```

The installer automatically creates this configuration file during installation using the access token embedded in the installation URL.

## Troubleshooting

### PowerShell Execution Policy

If you encounter execution policy errors, you can check the current policy:

```powershell
Get-ExecutionPolicy
```

To allow script execution for the current session only:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
```

### Check Installation Logs

If the installation fails, check the Windows Event Viewer:

1. Open **Event Viewer** (`eventvwr.msc`)
2. Navigate to **Windows Logs** > **Application**
3. Look for entries related to Lacework or FortiCNAPP

You can also check the installation directory for log files:
```
C:\ProgramData\Lacework\logs\
```

### Verify Connectivity

Ensure your Windows machine can reach the FortiCNAPP server:

```powershell
Test-NetConnection -ComputerName api.lacework.net -Port 443
```

## Uninstallation

To uninstall the FortiCNAPP agent:

1. Open **Control Panel** > **Programs and Features**
2. Find **Lacework Agent** or **FortiCNAPP Agent**
3. Click **Uninstall**

Alternatively, use PowerShell:

```powershell
Get-WmiObject -Class Win32_Product | Where-Object {$_.Name -like "*Lacework*"} | ForEach-Object {$_.Uninstall()}
```

Or use the uninstaller directly:
```powershell
C:\Program Files\Lacework\uninstall.exe
```

## Additional Resources

- [Install Windows Agent Documentation](https://docs.fortinet.com/document/lacework-forticnapp/latest/administration-guide/001455/download-the-windows-agent-installer)
- [Lacework Agent Documentation](https://docs.lacework.net/)

## Security Notes

- The installation script requires administrator privileges to install system services and configure the agent
- The access token is embedded in the installation URL and should be kept secure
- Always verify the source of the installation script before execution
- The agent runs as a Windows service with appropriate permissions to monitor system activity
- Configuration files are stored in a protected location with restricted access

