# Vagrant Network Configuration with DHCP Server

This repository provides a Vagrant configuration that sets up a virtual network environment. It includes a server configured with a DHCP server and multiple clients connected to different internal networks.

## Project Structure

- **server**: Configured with a static IP on multiple networks and installs a DHCP server.
- **clients**: Generated using a reusable function, which allows for easy creation of multiple clients on specified internal networks.

## Vagrantfile Overview

### Server Configuration

The server in this setup:
- Uses the `debian/bookworm64` box.
- Is assigned static IP addresses across two networks (`intnet1` and `intnet2`).
- Installs and configures the ISC DHCP Server to manage DHCP for connected clients.

### Client Configuration

The clients are created using a function to streamline the setup of multiple machines. Each client connects to a specified internal network and receives an IP address dynamically via DHCP.

## Files and Folders

- **Vagrantfile**: Defines the network configuration and provision settings.
- **shared/dhcp_settings**:
  - **isc-dhcp-server**: Default configuration file for the DHCP server.
  - **dhcpd.conf**: Main configuration file defining DHCP settings for `intnet1` and `intnet2`.

## Usage

1. **Install Vagrant**: Ensure [Vagrant](https://www.vagrantup.com/downloads) is installed on your system.
2. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/your-repo.git
   cd your-repo
