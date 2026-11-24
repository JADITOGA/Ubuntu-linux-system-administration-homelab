# LINUX SYSTEMS & INFRASTRUCTURE

<p align="center">
  <strong>Building. Configuring. Securing. Troubleshooting.</strong>
</p>

<p align="center">
  A hands-on homelab focused on Linux system administration, networking, infrastructure and security.
</p>

---

## `$ whoami`

I'm an aspiring IT systems administrator with a strong interest in Linux, networking and cybersecurity.

This repository documents my practical work in building and managing IT infrastructure using virtualized environments.

Rather than focusing exclusively on theory, I use this homelab to explore how systems work, configure services, investigate problems and understand the decisions behind an infrastructure setup.

My long-term objective is to develop the technical foundation required for a **Fachinformatiker für Systemintegration (FISI)** Ausbildung in Germany.

---

## `$ ls ./projects`

### 01 / Linux Company Environment

<sub>LINUX ADMINISTRATION · USER MANAGEMENT · SSH · WEB SERVICES</sub>

A simulated company environment built on Ubuntu Server.

The objective was to establish the foundations of a Linux-based IT environment, including user administration, permissions, shared resources and remote server access.

**Key implementations**
- User and group administration
- Linux permissions and ownership
- Shared company directories
- SSH remote administration
- Nginx web server deployment

[→ Explore Project 01](./Project-1-Linux-Company-Environment/)

---

### 02 / Linux Web Server Infrastructure

<sub>WEB HOSTING · NETWORK SECURITY · AUTOMATION · BACKUP & RECOVERY</sub>

An expansion of the original environment into a more complete web server infrastructure for the fictional company Musterfirma GmbH.

The objective was to host multiple websites while introducing encryption, network access controls, secure administration and automated backup procedures.

**Key implementations**
- Nginx virtual hosting
- HTTPS configuration using TLS
- UFW firewall rules
- SSH key-based authentication
- Bash backup automation
- Cron scheduling and logging
- Backup extraction and recovery testing

[→ Explore Project 02](./Project-2-Web-Server-Infrastructure/)

---

## `$ cat technical-stack.txt`

| Area | Technologies |
|---|---|
| Operating Systems | Ubuntu Server, Windows 11 |
| Virtualization | Oracle VirtualBox |
| Web Infrastructure | Nginx |
| Networking | TCP/IP, SSH, NAT |
| Security | UFW, OpenSSL, TLS |
| Automation | Bash, Cron |
| Administration | Linux CLI, systemd |
| Version Control | Git, GitHub |

---

## `$ cat engineering-principles.txt`

**Understand before configuring.**

Every project is an opportunity to understand how individual components interact, not simply make a service work.

**Troubleshoot, don't guess.**

Investigate errors, identify their causes and verify that the solution actually works.

**Security is part of the setup.**

Permissions, authentication, firewall policies and sensitive data handling should be considered from the beginning.

**Document the work.**

Record configurations, architecture, testing procedures and lessons learned so that the environment can be understood and maintained.

---

## `$ ./roadmap.sh`

Areas I intend to explore next:

- Linux service administration and monitoring
- DNS and DHCP infrastructure
- Network segmentation and VLANs
- Active Directory and Windows Server
- Centralized logging
- Advanced backup and disaster recovery
- Practical cybersecurity labs

---

<p align="center">
  <strong>BUILDING MY WAY INTO IT INFRASTRUCTURE.</strong>
  <br/>
  <sub>Hands-on projects · Continuous learning · Practical problem solving</sub>
</p>
