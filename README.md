# FortiCNAPP Agent Installation Guide for Linux

This guide provides step-by-step instructions for installing the FortiCNAPP agent on a Linux machine.

## Prerequisites

- A Linux machine running a 64-bit operating system
- Root or sudo access
- Internet connectivity
- wget installed on the system

## Getting the Installation URL

1. Log in to your FortiCNAPP console
2. Navigate to **Settings** > **Agent Tokens**
3. Click **Add New** > **Linux**
4. Click **Actions** > **Install**
5. Click **Copy URL** to copy the installation script URL

The URL will look like:
```
https://partner-demo.lacework.net/mgr/v1/download/<token>/install.sh
```

## Installation

On the target Linux machine, follow these steps:

1. Download the installation script using `wget`:
   ```bash
   wget <INSTALLATION_URL>
   ```

   Replace `<INSTALLATION_URL>` with the URL you copied from the FortiCNAPP console.

   **Example:**
   ```bash
   wget https://partner-demo.lacework.net/mgr/v1/download/e3221327f0b8e012de1ea0b688294cec0dafffb23ccebf7bca68b928/install.sh
   ```

2. Make the script executable:
   ```bash
   sudo chmod +x install.sh
   ```

3. Run the installation script:
   ```bash
   sudo ./install.sh
   ```

**Complete Example:**
```bash
wget https://partner-demo.lacework.net/mgr/v1/download/e3221327f0b8e012de1ea0b688294cec0dafffb23ccebf7bca68b928/install.sh
sudo chmod +x install.sh
sudo ./install.sh
```

## Installation Options

The installer supports several optional parameters:

- **`-h`**: Display usage information
- **`-v`**: Display script version
- **`-F`**: Disable File Integrity Monitoring (FIM)
- **`-S`**: Enable strict mode
- **`-O`**: Filter auditd related messages going to system journal
- **`-U <server_url>`**: Specify the server URL where the agent sends data
- **`-L`**: List downloadable agent versions
- **`-V <version>`**: Download a specific agent version
- **`-H <hash>`**: Provide RPM or DEB package hash

**Example with options:**
```bash
sudo ./install.sh -F -U https://api.lacework.net
```

## Verification

After installation, verify that the agent is running:

```bash
# Check agent status (systemd)
sudo systemctl status lacework

# Or check the service (if using init.d)
sudo service lacework status
```

## Configuration

The agent configuration file is located at:
```
/var/lib/lacework/config/config.json
```

The installer automatically creates this configuration file during installation using the access token embedded in the installation URL.

## Supported Operating Systems

The installer supports the following Linux distributions:

- **Debian/Ubuntu** (deb packages)
- **Red Hat/CentOS/Fedora** (rpm packages)
- **Alpine Linux** (apk packages)

For a complete list of supported platforms, visit:
https://docs.lacework.net/onboarding/supported-operating-systems#supported-operating-systems

## Troubleshooting

### Enable Verbose Output

To see detailed installation logs, set the `LaceworkVerbose` environment variable:

```bash
export LaceworkVerbose=true
sudo ./install.sh
```

### Check Installation Logs

If the installation fails, check the system logs:

```bash
# Check systemd logs
sudo journalctl -u lacework

# Check service logs
sudo tail -f /var/log/lacework/*
```

### Verify Connectivity

Ensure your Linux machine can reach the FortiCNAPP server:

```bash
wget --spider https://api.lacework.net
```

## Uninstallation

To uninstall the FortiCNAPP agent:

```bash
# For Debian/Ubuntu
sudo apt-get remove lacework

# For Red Hat/CentOS/Fedora
sudo yum remove lacework

# For Alpine Linux
sudo apk del lacework
```

## Additional Resources

- [FortiCNAPP Documentation](https://docs.fortinet.com/)
- [Lacework Agent Documentation](https://docs.lacework.net/)

## Security Notes

- The installation script requires root privileges to install system packages and configure services
- The access token is embedded in the installation URL and should be kept secure
- The agent runs with appropriate permissions to monitor system activity
- Configuration files are stored with restricted permissions (640)

