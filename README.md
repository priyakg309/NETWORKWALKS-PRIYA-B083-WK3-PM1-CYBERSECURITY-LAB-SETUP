# NetworkWalks B082 — Week 3 · Password Cracking

<p align="center">
  <img src="https://img.shields.io/badge/purpose-educational%20only-blue" alt="Educational">
  <img src="https://img.shields.io/badge/testing-authorized-success" alt="Authorized">
  <img src="https://img.shields.io/badge/tool-John%20the%20Ripper-red" alt="John the Ripper">
  <img src="https://img.shields.io/badge/tool-Johnny%20GUI-orange" alt="Johnny">
  <img src="https://img.shields.io/badge/tool-NetworkWalks%20Online%20Tools-purple" alt="NetworkWalks Tools">
  <img src="https://img.shields.io/badge/NetworkWalks-Week%203-red" alt="Week 3">
</p>

This repo documents **Week 3** of my Cybersecurity & Ethical Hacking internship with
NetworkWalks Academy (Batch B082). Week 3 is all about **password cracking** — recovering
the passwords of encrypted PDF files and confirming the results by opening them. It has
two parts, each using a different toolset for the same goal:

- **PM1 — Password Cracking with JTR:** using **John the Ripper (JTR)** and its graphical
  front-end **Johnny** — the industry-standard cracking tools.
- **PM2 — Password Cracking with NetworkWalks Tools:** using NetworkWalks' own free,
  browser-based **Hash Calculator** and **Password Cracker** — no installation needed.

Both modules follow the same idea: take the password hash out of a locked PDF, then run a
dictionary attack that tries word after word until one matches. Doing it two ways shows
that a professional CLI tool and a simple web tool rely on the **exact same underlying
technique** — and that a weak password falls to both in seconds.

---

## ⚠️ Authorization & Scope

All files cracked here are **practice PDFs provided by NetworkWalks** as part of the B082
internship — they are deliberately locked as a training (capture-the-flag) exercise.

**In scope:**
- The course-provided practice PDFs (`My Locked PDF1.pdf`, `PDF2`, `PDF3`), cracked on my
  own lab machine.

Nothing else was tested — no third-party files and no unauthorized systems, only the
training material I was given, on hardware I own and control.

---

## PM1 · Password Cracking with John the Ripper (JTR)

**John the Ripper (JTR)** is the industry-standard password cracker; **Johnny** is its
point-and-click GUI. The goal of this module was to recover the passwords of three locked
practice PDFs and open them to confirm.

### Tools
- **John the Ripper (jumbo)** — command-line cracker
- **Johnny** — JTR graphical front-end
- **Online PDF Hash Extractor** — https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php

### Steps

**1. Set up and verify John (CLI)**
<p align="center"><i>Install snap version of JTR CLI.</i></p>

**2. Open Johnny (GUI)** — Johnny runs John underneath, so it's pointed at a valid John
executable and reports the detected version.

<p align="center">
<p align="center"><i>Johnny detects John the Ripper 1.9.0-jumbo — ready for attacks.</i></p>

**3. Extract the PDF password hash** — upload each locked PDF to the online extractor. The
output **must start with `$pdf$`** (remove any `b'` prefix). Save each to its own file
(`hash1.txt`, `hash2.txt`, `hash3.txt`).

- https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php

</p>
<p align="center"><i>The locked PDF converted to its <code>$pdf$</code> hash.</i></p>

**4. Crack the hashes** — done in Johnny (*Open password file → Start new attack*).

</p>
<p align="center"><i>PDF 1 cracked → <b>password1</b>.</i></p>

<p align="center"><i>PDF 2 cracked → <b>password1</b>.</i></p>

<p align="center"><i>PDF 3 cracked → <b>1qaz2wsx</b>.</i></p>

**5. Verify — open the unlocked PDFs.** Each recovered password opened its PDF; PDF 3
revealed the flag.

<p align="center">
  <img src="W3-PM1-JTR/screenshots/Step7_All_Three_PDFs_Unlocked.png" width="800">
</p>
<p align="center"><i>All three PDFs unlocked with their recovered passwords.</i></p>

### Results — PM1

| PDF file            | Recovered password | Why it was weak                  |
|---------------------|--------------------|----------------------------------|
| My Locked PDF1.pdf  | `password1`        | one of the most common passwords |
| My Locked PDF2.pdf  | `password1`        | one of the most common passwords |
| My Locked PDF3.pdf  | `1qaz2wsx`         | keyboard-walk pattern            |


---

## PM2 · Password Cracking with NetworkWalks Online Tools

This module reaches the same goal using NetworkWalks' own **free, browser-based** tools —
no installation. It uses two tools in sequence, and proves the point that a simple web tool
uses the **same dictionary-attack idea** as John the Ripper.

### Tools
- **[NetworkWalks Hash Calculator](https://networkwalks.com/hash-calculator/)** — extracts
  the `$pdf$` crackable hash from a locked PDF (the PDF is parsed locally in the browser).
- **[NetworkWalks Password Cracker](https://networkwalks.com/password-cracker/)** — runs a
  dictionary attack, hashing each word in a wordlist and matching it against the PDF hash.

### Steps

**1. Open the lab task page** and download the locked practice PDF.

<p align="center">

<p align="center"><i>PM2 lab task — password cracking with NetworkWalks online tools.</i></p>

**2. Extract the hash** — in the Hash Calculator, open the **PDF** tab and upload the locked
PDF. It detects the encryption and outputs the `$pdf$` hash (Revision R4, Version V4,
128-bit key).

<p align="center"><i>Hash Calculator extracts the <code>$pdf$</code> hash from the locked PDF.</i></p>

**3. Run the dictionary attack** — paste the hash into the Password Cracker and start it.
It tries each word in the built-in wordlist until it finds a match.

<p align="center"><i>Dictionary attack matches the password → <b>password1</b>.</i></p>

**4. Verify — open the unlocked PDF** with the recovered password to reveal the flag.

<p align="center"><i>PDF unlocked with <b>password1</b> — flag captured.</i></p>

### Results — PM2

| PDF file           | Recovered password | Method                         |
|--------------------|--------------------|--------------------------------|
| My Locked PDF1.pdf | `password1`        | dictionary attack (built-in wordlist) |
| My Locked PDF2.pdf | `password1`        | dictionary attack (built-in wordlist) |
| My Locked PDF1.pdf | `1qaz2wsx`        | dictionary attack (built-in wordlist) |


---

## Author

Priya Kishore Gehani
Networkwalks - Cybersecurity 
Week 3 - B083
