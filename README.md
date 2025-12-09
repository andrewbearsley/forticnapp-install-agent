# FortiCNAPP Agent Installation Guides

This repository contains installation guides for the FortiCNAPP agent on different operating systems.

## Installation Guides

- **[Linux Installation Guide](INSTALL-LINUX.md)** - Step-by-step instructions for installing the FortiCNAPP agent on Linux systems
- **[Windows Installation Guide](INSTALL-WINDOWS.md)** - Step-by-step instructions for installing the FortiCNAPP agent on Windows systems

## Quick Start

### Linux Installation

1. Get the installation URL from **Settings** > **Agent Tokens** > **Add New** > **Linux** > **Actions** > **Install**
2. Download and run the installation script:

```bash
wget <INSTALLATION_URL>
sudo chmod +x install.sh
sudo ./install.sh
```

### Windows Installation

1. Download the MSI installer from **Settings** > **Configuration** > **Agent Installation**
2. Get the access token from **Settings** > **Agent Tokens** > **Add New** > **Windows**
3. Install using msiexec:

```cmd
msiexec /i LWDataCollector.msi ACCESSTOKEN=<access_token> SERVERURL=https://api.lacework.net
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

## Additional Resources

- [Install Linux Agent Documentation](https://docs.fortinet.com/document/forticnapp/latest/administration-guide/6960/linux-agent-based-workload-security)
- [Install Windows Agent Documentation](https://docs.fortinet.com/document/forticnapp/latest/administration-guide/876164/windows-agent-based-workload-security)

## Support

For issues or questions, please refer to the official FortiCNAPP documentation or contact Fortinet support.
