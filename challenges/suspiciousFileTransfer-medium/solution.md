# Solution — Suspicious File Transfer

## Tools

Kali Linux with `tshark`, `file` and `gzip`.

## Step 1: Inspect the capture

```bash
tshark -r traffic.pcap -q -z conv,tcp
```

List HTTP responses:

```bash
tshark -r traffic.pcap -Y 'http.response' -T fields -e tcp.stream -e ip.src -e http.content_type
```

Look for unusual binary file transfers.

## Step 2: Reconstruct HTTP files

```bash
mkdir extracted
tshark -r traffic.pcap --export-objects http,extracted
```

List the extracted files:

```bash
ls -l extracted/
file extracted/*
```

The relevant transfer is `/downloads/report.dat` from `203.0.113.72`.

Despite its `.dat` extension, the file contains gzip-compressed data.

## Step 3: Recover the flag

```bash
gzip -dc extracted/report.dat
```

Expected output:

```text
INTERNAL TRAINING RECORD
File ID: 8031
Incident token: CTF{reconstruct_the_compressed_transfer}
```

**Flag:** `CTF{reconstruct_the_compressed_transfer}`

## Why Medium?

The participant needs to:

1. Analyze several network connections and identify the relevant transfer.
2. Reconstruct the HTTP object.
3. Identify the file format and decompress the data.

The challenge combines HTTP traffic analysis and file-format identification using several command-line tools.

Estimated solving time: 30–60 minutes for students with basic security knowledge, to be confirmed by playtesting.