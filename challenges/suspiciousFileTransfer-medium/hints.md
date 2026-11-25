# Hints — Suspicious File Transfer

**Hint 1:**

Not all HTTP traffic in the capture is suspicious. Look for external destinations and examine custom HTTP headers that might indicate a multi-part upload.

**Hint 2:**

The suspicious data was split into multiple fragments and uploaded separately. Each fragment has headers indicating its position in the sequence (`X-Part`, `X-Total`, `X-Upload-ID`).

**Hint 3:**

After extracting and reassembling all fragments in the correct order, check the file format with the `file` command. The data is compressed using a common algorithm.