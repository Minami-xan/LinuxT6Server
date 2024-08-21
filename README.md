# T6 Server - Plutonium Black Ops II Server Installer

![Version](https://img.shields.io/badge/Version-2.1.0-blue)
![Debian](https://img.shields.io/badge/Debian-10%20%7C%2011%20%7C%2012-brightgreen?logo=Debian)
![Plutonium T6](https://img.shields.io/badge/Plutonium-T6-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)
![GitHub repo size](https://img.shields.io/github/repo-size/Sterbweise/T6Server)
![GitHub stars](https://img.shields.io/github/stars/Sterbweise/T6Server)
![GitHub forks](https://img.shields.io/github/forks/Sterbweise/T6Server)
![GitHub issues](https://img.shields.io/github/issues/Sterbweise/T6Server)
![GitHub last commit](https://img.shields.io/github/last-commit/Sterbweise/T6Server)

<img src="https://imgur.com/bBrx8Hf.png" alt="Plutonium Logo" width="350"/>

T6 Server is a comprehensive management suite for setting up and running Plutonium Call of Duty: Black Ops II servers on Debian-based systems. This project aims to simplify the process of installing, configuring, and managing T6 servers, making it accessible to both beginners and experienced server administrators.

## Table of Contents

- [T6 Server - Plutonium Black Ops II Server Management Suite](#t6-server---plutonium-black-ops-ii-server-management-suite)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Prerequisites](#prerequisites)
    - [System Requirements](#system-requirements)
    - [Software Requirements](#software-requirements)
    - [Network Requirements](#network-requirements)
    - [Additional Considerations](#additional-considerations)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Launching the Server](#launching-the-server)
  - [Troubleshooting](#troubleshooting)
    - [Wine Display Errors](#wine-display-errors)
    - [Unable to Load Import from binkw32.dll](#unable-to-load-import-from-binkw32dll)
    - [Server Not Appearing in Plutonium Server List](#server-not-appearing-in-plutonium-server-list)
    - [Authentication Issues](#authentication-issues)
  - [Documentation](#documentation)
  - [Contributing](#contributing)
    - [Submitting Pull Requests](#submitting-pull-requests)
    - [Ideas for Contributions](#ideas-for-contributions)
    - [Reporting Issues](#reporting-issues)
    - [Improving Documentation](#improving-documentation)
    - [Code Review](#code-review)
  - [Roadmap](#roadmap)
    - [Short-term Goals (1-3 months)](#short-term-goals-1-3-months)
    - [Medium-term Goals (3-6 months)](#medium-term-goals-3-6-months)
  - [License](#license)
  - [Acknowledgements](#acknowledgements)
  - [Support](#support)

## Features

- Easy installation process
- Automated system updates and dependency management
- Firewall configuration with UFW
- Wine installation for running Windows applications
- .NET installation for IW4MAdmin support
- Localization support (English and French)
- Server binary installation and configuration
- User-friendly command-line interface

## Prerequisites

### System Requirements
- **Operating System:** Debian 10, 11, or 12 (64-bit)
- **Architecture:** x86_64 (AMD64)
- **RAM:** Minimum 512MB, 2GB recommended
- **Storage:** At least 10GB of free disk space

### Software Requirements
- **Root Access:** Full system privileges (root or sudo)
- **Package Manager:** apt (comes pre-installed on Debian)
- **Git:** For cloning the repository

If you don't have sudo or git installed, you can install them as follows:

1. To install sudo (as root):
   ```bash
   apt install sudo
   ```

2. To install git:
   ```bash
   sudo apt install git
   ```

These commands will ensure you have the necessary software to proceed with the installation.

### Network Requirements
- **Internet Connection:** Stable broadband connection
- **Firewall:** Ability to open and forward necessary ports
- **Static IP:** Recommended for consistent server accessibility

### Additional Considerations
- Basic familiarity with Linux command line
- Understanding of server administration concepts
- Willingness to troubleshoot potential issues

Ensure all prerequisites are met before proceeding with the installation to guarantee a smooth setup process.

## Installation

1. Navigate to the /opt directory:
   ```bash
   cd /opt
   ```

2. Clone the repository:
   ```bash
   git clone https://github.com/Sterbweise/T6Server.git
   ```

3. Navigate to the T6Server directory:
   ```bash
   cd T6Server
   ```

4. Make the installation script executable:
   ```bash
   chmod +x install.sh
   ```

5. Run the installation script:
   ```bash
   sudo ./install.sh
   ```

6. Follow the on-screen instructions to complete the installation. The script will guide you through:
   - Language selection
   - UFW firewall installation and configuration
   - SSH port configuration
   - .NET installation (optional, required for IW4MAdmin)
   - Wine installation
   - Game binary installation

## Configuration

After installation, the primary configuration file to modify is `/opt/T6Server/T6Server.sh`. This file contains essential settings for your Plutonium Call of Duty: Black Ops II server. Below are the key variables you should configure:

| Variable    | Description                                           | Default Value              |
|-------------|-------------------------------------------------------|----------------------------|
| SERVER_NAME | The name of your server as it appears in server lists | "SERVER_NAME"              |
| GAME_PATH   | Path to your game files (Multiplayer or Zombie mode)  | "/opt/T6Server/Server/Multiplayer" |
| SERVER_KEY  | Your unique Plutonium server key                      | "YOURKEY"                  |
| CONFIG_FILE | Server configuration file (mode-specific)             | "dedicated.cfg"            |
| SERVER_PORT | UDP port your server will listen on                   | 4976                       |
| GAME_MODE   | Game mode selection ("t6mp" or "t6zm")                | "t6mp"                     |

To configure your server:

1. Open the configuration file:
   ```bash
   nano /opt/T6Server/T6Server.sh
   ```

2. Modify the variables according to your preferences. For example:
   ```bash
   readonly SERVER_NAME="My Awesome T6 Server" # The name of your server
   readonly SERVER_KEY="your_server_key" # Key provided by Plutonium
   readonly SERVER_PORT=4976 # Default port for T6 servers
   readonly GAME_MODE="t6mp" # "t6mp" for Multiplayer, "t6zm" for Zombies
   ```

3. Save the file and exit the editor by pressing `Ctrl+x`, then `Y` to confirm, and Enter to save.

Note: For Zombie mode, set `GAME_PATH` to "/opt/T6Server/Server/Zombie", `CONFIG_FILE` to "dedicated_zm.cfg", and `GAME_MODE` to "t6zm".

Ensure all settings are correctly configured before launching your server.

## Launching the Server

To launch your Plutonium Call of Duty: Black Ops II server, follow these professional steps:

1. Navigate to the T6Server installation directory:
   ```bash
   cd /opt/T6Server
   ```

2. Ensure the start script has the necessary execution permissions:
   ```bash
   sudo chmod +x T6Server.sh
   ```

3. Launch the server:
   ```bash
   ./T6Server.sh
   ```

For advanced server management:
- To run multiple servers concurrently, utilize terminal multiplexers such as `tmux` or `screen`.
- For background operation, you can use the `nohup` command:
  ```bash
  nohup ./T6Server.sh > server.log 2>&1 &
  ```
  This will run the server in the background, redirecting output to `server.log`.

Note: Ensure all necessary configurations in `server.cfg` and other relevant files are properly set before launching the server.

## Troubleshooting

This section provides solutions to common issues you may encounter while setting up and running your Plutonium Call of Duty: Black Ops II server. Follow these detailed steps to resolve problems efficiently.

### Wine Display Errors

**Issue**: You may see error messages related to Wine display when starting the server.

**Solution**: These errors are not critical and can be safely ignored. The Plutonium server operates as a console application and does not require graphical support. Your server will function correctly despite these messages.

**Note for debugging**: By default, Wine errors are hidden. If you need to debug Wine-related issues, you can remove the `2>/dev/null` at the end of the server start command in `T6Server.sh`. This will allow Wine errors to be displayed, which can be helpful for troubleshooting.

### Unable to Load Import from binkw32.dll

**Issue**: An error occurs when the server attempts to load binkw32.dll.

**Solution**: 
1. Verify the `PAT` variable in `T6Server.sh`:
   - Open the file: `nano /opt/T6Server/T6Server.sh`
   - Ensure the `PAT` variable is correctly set to your server's path, pointing to the directory containing binkw32.dll:
     - For Multiplayer: `/opt/T6Server/Server/Multiplayer`
     - For Zombie mode: `/opt/T6Server/Server/Zombie`
2. Correct file permissions:
   ```bash
   sudo chmod -R 755 /opt/T6Server
   ```
3. If the issue persists, try reinstalling the game binaries using the installation script.

### Server Not Appearing in Plutonium Server List

**Issue**: Your server is running but not visible to players in the Plutonium server list.

**Solution**:
1. Verify port accessibility:
   - Ensure the server port (default: 4976) is open for UDP traffic
   - Use a port checking tool to confirm the port is reachable from the internet
2. Configure your firewall:
   ```bash
   sudo ufw allow 4976/udp comment "Plutonium-Server"
   sudo ufw reload
   ```
3. If behind a NAT:
   - Configure port forwarding on your router
   - Forward UDP port 4976 to your server's local IP address
4. Verify server configuration:
   - Check `server.cfg` for correct settings
   - Ensure `sv_lanOnly` is set to 0

### Authentication Issues

**Issue**: You encounter authentication errors when starting the server.

**Solution**:
1. Verify your Plutonium key:
   - Log in to your Plutonium account at https://platform.plutonium.pw/serverkeys
   - Confirm your key is valid and not expired
2. Check key placement:
   - Open `T6Server.sh`
   - Ensure the `SERVER_KEY` variable contains your correct key
3. If issues persist:
   - Reinstall game binaries using the installation script
   - Update Plutonium to the latest version

For additional assistance, consult the [Plutonium forums](https://forum.plutonium.pw/) or join the [Plutonium Discord](https://discord.gg/plutonium) community.

## Documentation

For more detailed information on server configuration, configuration options, and advanced features, please refer to our [Wiki](https://github.com/Sterbweise/T6Server/wiki).

## Contributing

We welcome and appreciate contributions from the community! Here are some ways you can contribute to the T6 Server project:

### Submitting Pull Requests

1. Fork the repository and create your branch from `main`.
2. If you've added code that should be tested, add tests.
3. Ensure your code follows the existing style to maintain consistency.
4. Update the documentation if you've made changes that affect it.
5. Write a clear and descriptive commit message.
6. Open a pull request with a comprehensive description of the changes.

### Ideas for Contributions

- Implement additional server configuration options
- Improve error handling and logging
- Enhance the user interface of the management scripts
- Optimize server performance
- Improve compatibility with different Debian versions or other Linux distributions
- Create additional language localizations

### Reporting Issues

- Use the GitHub issue tracker to report bugs
- Provide a clear and detailed description of the issue
- Include steps to reproduce the problem
- Specify your operating system and relevant software versions

### Improving Documentation

- Help improve the README, wiki, or inline code documentation
- Write tutorials or guides for setting up and managing servers
- Create or improve troubleshooting guides

### Code Review

- Review pull requests from other contributors
- Provide constructive feedback and suggestions

We strive to make contributing to T6 Server a positive experience for everyone.

Thank you for helping make T6 Server better!

## Roadmap

Our roadmap for T6 Server focuses on enhancing stability, improving user experience, and expanding functionality. Here's what we're planning:

### Short-term Goals (1-3 months)

- [ ] Resolve installation issues on various Debian-based distributions
  - [ ] Fix dependency conflicts
  - [ ] Improve error handling during installation
  - [ ] Create detailed troubleshooting guides
- [ ] Enhance debugging capabilities
  - [ ] Implement verbose logging options
  - [ ] Create a diagnostic tool for common issues
- [ ] Optimize server performance
  - [ ] Reduce resource usage
  - [ ] Improve startup and shutdown times

### Medium-term Goals (3-6 months)

- [ ] Simplify multi-server management
- [ ] Enhance configuration options
  - [ ] Add more customizable server settings
  - [ ] Create configuration templates for popular game modes
- [ ] Improve update mechanism
  - [ ] Implement automatic updates with rollback capability
  - [ ] Add delta updates to reduce bandwidth usage

I'm committed to continuously improving T6 Server based on user feedback and community needs. If you encounter any issues or have suggestions, please don't hesitate to open an issue or contribute to the project!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

We would like to express our sincere gratitude to the following projects and their creators for their invaluable contributions to the T6 Server project:

- [Plutonium](https://plutonium.pw): For their exceptional work on the T6 client and server, which forms the foundation of our project. Their dedication to preserving and enhancing classic Call of Duty titles is commendable.

- [IW4MAdmin](https://github.com/RaidMax/IW4M-Admin): We extend our thanks to RaidMax and the IW4MAdmin team for their comprehensive administration tools. Their robust solution significantly enhances server management capabilities.

- [plutonium-updater](https://github.com/mxve/plutonium-updater.rs): Special recognition goes to mxve for developing the plutonium-updater. This tool has been instrumental in streamlining our server update process, ensuring that our servers always run the latest version with minimal downtime.

These projects have been crucial in the development and ongoing improvement of T6 Server. We are deeply appreciative of the hard work and dedication of all contributors involved in these projects.

## Support

For support, please contact:

- Email: [contact@sterbweise.dev](mailto:contact@sterbweise.dev)
- Telegram: [@SG991](https://t.me/SG991)

You can also open an issue on this repository for bug reports or feature requests.

---

Developed with ❤️ by [Sterbweise](https://github.com/Sterbweise)
