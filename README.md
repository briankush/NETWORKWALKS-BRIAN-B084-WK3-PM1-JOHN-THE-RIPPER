# Password Cracking with John the Ripper on Kali Linux

This lab documents how to recover a weak password from a protected PDF using John the Ripper in Kali Linux. It was completed as part of cybersecurity coursework with [Networkwalks Academy](https://www.networkwalks.com).

The original exercise used the Johnny GUI on Windows. This write-up provides the equivalent workflow for Kali Linux's command line.

## Objective

- Extract the password hash from `My Locked PDF1.pdf`.
- Use John the Ripper to test candidate passwords.
- Confirm that the recovered password unlocks the PDF.
- Demonstrate why weak and common passwords are vulnerable to cracking.

> **Authorization:** Only crack files that you own or have explicit permission to test.

## Environment

| Item | Detail |
| --- | --- |
| Operating system | Kali Linux |
| Tool | John the Ripper |
| Target | `My Locked PDF1.pdf` |
| Hash format | PDF hash beginning with `$pdf$` |

John the Ripper is included with Kali Linux, so installation is not required for this lab.

## Procedure

### 1. Extract the PDF hash

Upload the PDF to an authorized PDF hash extractor or use a local PDF-to-hash utility. Save the resulting hash in a file named `hash1.txt`.

The file should contain only the hash and begin with `$pdf$`. Remove any extra leading text or labels if they are present.

Example:

```text
$pdf$...
```

### 2. Verify John the Ripper

Confirm that John is available:

```bash
john --list=build-info
```

### 3. Crack the password

Run John against the extracted hash:

```bash
john hash1.txt
```

John detects the PDF hash format and tries its configured wordlists and mangling rules.

### 4. Display the result

Retrieve the recovered credentials after John finishes:

```bash
john --show hash1.txt
```

The expected result is:

```text
My Locked PDF1.pdf:password1
```

### 5. Unlock the PDF

Open `My Locked PDF1.pdf` and enter `password1` as the password. The PDF should unlock successfully.

## Result

The recovered password was `password1`. It is short, predictable, and matches a common password pattern, allowing John the Ripper to recover it quickly.

## Key Takeaways

- Password strength matters: weak passwords can be tested rapidly.
- Use a long, random, and unique password for sensitive documents.
- Prefer a reputable password manager to generate and store passwords.
- Keep sensitive files away from public upload and conversion services.