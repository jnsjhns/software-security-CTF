# Hidden Evidence — Hints

**Category:** Forensics  
**Difficulty:** Easy

### Hint 1 — Where to Look
*Small hint*

Not everything an image contains is visible when you open it.

### Hint 2 — What to Investigate
*Medium hint*

Image files can contain additional information beyond their pixels. Have you checked the file's metadata?

### Hint 3 — Which Tool to Use
*Strong hint*

Try inspecting the image with a metadata analysis tool such as `exiftool`.

```bash
exiftool evidence.png
```

Look carefully at the output.