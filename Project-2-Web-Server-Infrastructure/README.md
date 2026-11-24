# Project 2: Linux Web Server Infrastructure

## Overview

This project expands the Linux company environment built in Project 1 into a more complete web server infrastructure for a fictional company, **Musterfirma GmbH**.

The objective was to configure and secure an Ubuntu Server environment capable of hosting multiple websites, providing encrypted HTTPS connections, controlling network access, supporting secure remote administration, and performing automated backups.

The project was completed using Ubuntu Server running inside Oracle VirtualBox.

## Business Scenario

Musterfirma GmbH needs an internal IT infrastructure to host its company websites and IT portal.

As the system administrator, my task was to build and maintain a server environment that provides:

- Reliable website hosting.
- Secure HTTPS connections.
- Controlled incoming network traffic.
- Secure remote administration.
- Automated backups and recovery capabilities.

## Technologies Used

| Technology | Purpose |
|---|---|
| Ubuntu Server | Server operating system |
| VirtualBox | Virtualization |
| Nginx | Web server and virtual hosting |
| OpenSSL | TLS certificate generation |
| UFW | Firewall management |
| OpenSSH | Secure remote administration |
| Bash | Backup automation |
| Cron | Scheduled backups |
| tar | Backup archiving |

## Implemented Features

### 1. Multi-site Web Hosting
Configured Nginx to host multiple websites using separate server blocks and document roots.

### 2. HTTPS / TLS
Configured HTTPS using a self-signed TLS certificate generated with OpenSSL.

### 3. Firewall Configuration
Configured UFW with a default-deny incoming policy and explicit rules for required services.

### 4. SSH Hardening
Configured SSH key-based authentication and disabled password authentication for remote SSH access.

### 5. Automated Backups
Created a Bash script to back up website files and Nginx configuration files.

### 6. Recovery Testing
Extracted a backup into a temporary directory to verify that the archived website files could be recovered.

### 7. Backup Scheduling and Logging
Configured a daily Cron job to execute the backup script at 02:00 and record its output in a log file.

## Project Structure

Documentation, configuration examples, screenshots and diagrams will be organized in this directory.

## Security Considerations

- SSH password authentication is disabled.
- Incoming traffic is restricted using UFW.
- The TLS certificate's private key is protected with restrictive file permissions.
- Backup archives are stored in a root-protected directory.
- Private keys and sensitive backup archives are not included in this repository.

## Limitations and Future Improvements

- The TLS certificate is self-signed and is not trusted by default by web browsers.
- Backups are stored on the same virtual machine, so they do not protect against complete VM or disk loss.
- Future improvements could include off-site backups, certificate management and more advanced monitoring.

## Status

**Project implementation completed. Documentation and portfolio preparation in progress.**
