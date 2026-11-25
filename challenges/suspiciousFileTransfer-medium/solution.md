# Solution — Suspicious File Transfer

## Tools Required

- `tshark` or Wireshark
- `file` command
- `gzip`
- Python 3 with `scapy` (for automated solution)

## Overview

The challenge requires identifying suspicious HTTP POST requests among normal traffic, extracting multi-part upload fragments, reassembling them in the correct order, and decompressing the result to find the flag.

---

## Solution Method 1: Manual Analysis with tshark

### Step 1: Initial Traffic Analysis

```bash
tshark -r traffic.pcap -q -z conv,tcp
```

This shows all TCP conversations. Notice multiple HTTP connections.

### Step 2: Identify HTTP Traffic

```bash
tshark -r traffic.pcap -Y 'http.request' -T fields -e frame.number -e ip.dst -e http.host -e http.request.method -e http.request.uri
```

Look for suspicious patterns:
- External destination: `203.0.113.72` (collector-sync.example.test)
- Multiple POST requests to `/api/events`
- Custom headers suggesting multi-part uploads

### Step 3: Examine HTTP Headers

```bash
tshark -r traffic.pcap -Y 'http.request and http.host == "collector-sync.example.test"' -V
```

Notice the custom headers:
- `X-Upload-ID: a7f39c`
- `X-Part: 0, 1, 2, 3, 4`
- `X-Total: 5`

This indicates 5 fragments of a single upload.

### Step 4: Extract TCP Streams

Identify the stream numbers for each fragment:

```bash
tshark -r traffic.pcap -Y 'http.request and http.host == "collector-sync.example.test"' -T fields -e tcp.stream -e http.file_data | head
```

For each stream with the target Upload-ID, extract the HTTP body:

```bash
tshark -r traffic.pcap -Y 'tcp.stream == X' -T fields -e http.file_data | xxd -r -p > part_N.bin
```

Repeat for all 5 parts (check each stream number).

### Step 5: Concatenate Fragments

```bash
cat part_0.bin part_1.bin part_2.bin part_3.bin part_4.bin > combined.bin
```

### Step 6: Identify File Format

```bash
file combined.bin
```

Output: `gzip compressed data`

### Step 7: Decompress and Recover Flag

```bash
gzip -dc combined.bin
```

Output:
```
CONFIDENTIAL INCIDENT REPORT
Case ID: 8031
Incident token: CTF{reconstruct_the_compressed_transfer}
Record 000: event=XXXXX status=XXXX
...
```

**Flag:** `CTF{reconstruct_the_compressed_transfer}`

---

## Solution Method 2: Automated Python Script

For solution verification, use the included `extractAndGlue.py` script (located in `generate/` directory, **not provided to participants**):

```bash
cd generate/
python3 extractAndGlue.py
```

The script:
1. Reads the PCAP file
2. Filters HTTP POST requests with `X-Upload-ID: a7f39c`
3. Extracts body fragments and sorts by `X-Part` number
4. Reassembles and decompresses the data
5. Displays the flag

**Script output:**
```
[*] Extracting fragments from PCAP...
[+] Found 5 fragments
[*] Reassembling and decompressing...
============================================================
CONFIDENTIAL INCIDENT REPORT
Case ID: 8031
Incident token: CTF{reconstruct_the_compressed_transfer}
...
============================================================

[+] FLAG FOUND: CTF{reconstruct_the_compressed_transfer}
```

---

## Why Medium Difficulty?

The participant must:

1. **Identify suspicious traffic** among legitimate connections (telemetry, DNS, browsing)
2. **Understand multi-part uploads** by examining custom HTTP headers
3. **Extract and reassemble fragments** in correct order across multiple TCP streams
4. **Identify compressed format** and decompress the data

This requires knowledge of:
- HTTP protocol analysis
- TCP stream reconstruction
- File format identification
- Working with compressed data
- Command-line tools (`tshark`, `gzip`, `file`)

**Estimated solving time:** 30–60 minutes for students with intermediate networking and security knowledge.

**Skills validated:**
- Network forensics
- Protocol analysis
- Data exfiltration detection
- Multi-step problem solving