# FortiCNAPP Agent Installation Guides

This repository contains installation guides for the FortiCNAPP agent on different operating systems.

## Installation Guides

- **[Linux Installation Guide](INSTALL-LINUX.md)** - Step-by-step instructions for installing the FortiCNAPP agent on Linux systems
- **[Windows Installation Guide](INSTALL-WINDOWS.md)** - Step-by-step instructions for installing the FortiCNAPP agent on Windows systems

## Quick Start

### Getting the Installation URL

1. Log in to your FortiCNAPP console
2. Navigate to **Settings** > **Agent Tokens**
3. Click **Add New** > Select your platform (**Linux** or **Windows**)
4. Click **Actions** > **Install**
5. Click **Copy URL** to copy the installation script URL

### Linux Installation

```bash
wget <INSTALLATION_URL>
sudo chmod +x install.sh
sudo ./install.sh
```

### Windows Installation

```powershell
Invoke-WebRequest -Uri "<INSTALLATION_URL>" -OutFile "install.ps1"
Set-ExecutionPolicy Bypass -Scope Process -Force
.\install.ps1
```

## Prerequisites

### Linux
- 64-bit Linux operating system
- Root or sudo access
- Internet connectivity
- `wget` installed

### Windows
- Supported Windows version
- Administrator privileges
- Internet connectivity
- PowerShell (pre-installed)

## Additional Resources

- [Install Linux Agent Documentation](https://docs.fortinet.com/document/forticnapp/latest/administration-guide/6960/linux-agent-based-workload-security)
- [Install Windows Agent Documentation](https://docs.fortinet.com/document/forticnapp/latest/administration-guide/876164/windows-agent-based-workload-security)

## Support

For issues or questions, please refer to the official FortiCNAPP documentation or contact Fortinet support.
