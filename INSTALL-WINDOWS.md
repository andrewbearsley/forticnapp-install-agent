# FortiCNAPP Agent Installation Guide for Windows

This guide provides step-by-step instructions for installing the FortiCNAPP agent on a Windows machine.

## Prerequisites

- A Windows machine running a supported version of Windows
- Administrator privileges on the machine
- Internet connectivity

## Getting Installation Files and Token

### Download the MSI Installer

1. Log in to your FortiCNAPP console
2. Navigate to **Settings** > **Configuration** > **Agent Installation**
3. Locate the Windows agent MSI download link
4. Download the MSI installer (typically named `LWDataCollector.msi`) to your local machine

### Get the Access Token

1. In the FortiCNAPP Console, navigate to **Settings** > **Agent Tokens**
2. Click **Add New** > **Windows**
3. Enter a name for the token (optional: add a description)
4. Click **Save** to generate the token
5. Click the actions menu next to the token and select **Copy** to copy the access token

### Get the Server URL

The server URL (API endpoint) is typically:
```
https://api.lacework.net
```

For specific account endpoints, check your FortiCNAPP console settings.

## Installation

On the target Windows machine, follow these steps:

1. **Open Command Prompt as Administrator**:
   - Click on the **Start** menu
   - Type `cmd`
   - Right-click on **Command Prompt** and select **Run as administrator**

2. **Navigate to the directory containing the MSI installer**:
   ```cmd
   cd <path-to-msi-file>
   ```

3. **Install the agent using msiexec**:
   ```cmd
   msiexec /i LWDataCollector.msi ACCESSTOKEN=<access_token> SERVERURL=<server_url>
   ```

   Replace:
   - `<access_token>` with the access token you copied from the FortiCNAPP console
   - `<server_url>` with your API endpoint (typically `https://api.lacework.net`)

   **Example:**
   ```cmd
   msiexec /i LWDataCollector.msi ACCESSTOKEN=Your_Access_Token_Here SERVERURL=https://api.lacework.net
   ```

4. **Optional: Disable automatic upgrades during installation**:
   ```cmd
   msiexec /i LWDataCollector.msi ACCESSTOKEN=<access_token> SERVERURL=<server_url> AUTOUPGRADE=disabled
   ```

**Complete Example:**
```cmd
cd C:\Downloads
msiexec /i LWDataCollector.msi ACCESSTOKEN=Your_Access_Token_Here SERVERURL=https://api.lacework.net
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

The installer automatically creates this configuration file during installation using the access token and server URL provided during MSI installation.

## Troubleshooting

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

- The MSI installer requires administrator privileges to install system services and configure the agent
- The access token is provided as a parameter during installation and should be kept secure
- Always verify the source of the MSI installer before execution
- The agent runs as a Windows service with appropriate permissions to monitor system activity
- Configuration files are stored in a protected location with restricted access

