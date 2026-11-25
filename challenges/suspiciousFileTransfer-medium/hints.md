# Hints — Suspicious File Transfer

**Hint 1:**

Not every network connection is important. Focus on HTTP traffic and look for transferred files.

**Hint 2:**

Wireshark and tshark can reconstruct HTTP objects from packet captures. You do not necessarily need to examine every packet individually.

**Hint 3:**

Inspect the recovered file's actual format rather than trusting its extension. The transferred data may be compressed.