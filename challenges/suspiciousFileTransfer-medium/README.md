# Suspicious File Transfer

**Category:** Network  
**Difficulty:** Medium  
**Flag format:** `CTF{...}`

## Scenario

The security team detected unusual outbound network activity from an employee's workstation. A packet capture was collected during the incident.

The captured traffic contains multiple HTTP connections to different servers. Some appear to be legitimate internal telemetry, DNS queries, and routine browsing activity. However, one series of connections looks suspicious.

Your task is to analyze the network capture, identify the suspicious file transfer, and recover the confidential incident token that was exfiltrated.

## Provided file

`traffic.pcap`

## Objective

Find and submit the hidden flag.

## Skills tested

- HTTP traffic analysis
- TCP stream reconstruction
- File format identification
- Multi-part data reassembly
- Working with compressed data
