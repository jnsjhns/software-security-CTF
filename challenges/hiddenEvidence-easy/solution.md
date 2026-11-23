# Hidden Evidence — Solution

## Challenge Information

- **Category:** Forensics
- **Difficulty:** Easy
- **Flag:** `CTF{metadata_leaks_secrets}`
- **Supported Platforms:** Windows, Linux, macOS

## 1. Security Concept

PNG files can store additional information in metadata fields that are not visible when viewing the image.

In this challenge, the flag is embedded in the PNG textual metadata field `Comment`.

## 2. Prerequisites

**Required tool:** ExifTool

Installation depends on the operating system:

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install libimage-exiftool-perl
```

**Windows:**

Download ExifTool from https://exiftool.org/ and follow the official Windows installation instructions. Ensure that `exiftool.exe` is accessible from PowerShell, either through its full path or via the system PATH.

**macOS (Homebrew):**
```bash
brew install exiftool
```

## 3. Step-by-Step Solution

### Step 1 — Inspect the Image

Open `evidence.png` using any image viewer.

The image contains an internal security report but no visible flag.

### Step 2 — Analyze Metadata

Open a terminal in the directory containing `evidence.png`.

**Linux / macOS:**
```bash
exiftool evidence.png
```

**Windows (PowerShell):**
```powershell
exiftool.exe .\evidence.png
```

Both commands display the image's metadata.

### Step 3 — Identify the Flag

Look for the `Comment` field:

```text
Comment : CTF{metadata_leaks_secrets}
```

Alternatively, retrieve only that field:

**Linux / macOS:**
```bash
exiftool -Comment evidence.png
```

**Windows (PowerShell):**
```powershell
exiftool.exe -Comment .\evidence.png
```

### Step 4 — Submit the Flag

The recovered flag is:

`CTF{metadata_leaks_secrets}`

Submit it to the CTF platform.

## 4. Alternative Solution

Because the flag is stored as an uncompressed PNG text metadata entry, it may also be recovered using a tool that extracts printable strings, such as GNU `strings`.

On systems where GNU `strings` is installed:

```bash
strings evidence.png
```

This method is not guaranteed for all PNG metadata encodings, but works with the uncompressed textual metadata used in this implementation.

## 5. Difficulty Justification

- **Required Knowledge:** Basic file metadata concepts
- **Analysis:** Straightforward inspection
- **Solution Steps:** One primary investigation technique
- **Tools:** Standard forensic metadata tool
- **Estimated Time:** 5–15 minutes

**Difficulty: Easy**

## 6. Security Takeaway

Image metadata can expose information that is not visible in the displayed image.

Inspecting or removing unnecessary metadata before sharing files helps prevent accidental information disclosure.