# NetworkWalks B083 — Week 3 · Password Cracking

<p align="center">
  <img src="https://img.shields.io/badge/purpose-educational%20only-blue" alt="Educational">
  <img src="https://img.shields.io/badge/testing-authorized-success" alt="Authorized">
  <img src="https://img.shields.io/badge/tool-John%20the%20Ripper-red" alt="John the Ripper">
  <img src="https://img.shields.io/badge/tool-Johnny%20GUI-orange" alt="Johnny">
  <img src="https://img.shields.io/badge/tool-NetworkWalks%20Online%20Tools-purple" alt="NetworkWalks Tools">
  <img src="https://img.shields.io/badge/NetworkWalks-Week%203-red" alt="Week 3">
</p>

This repo documents **Week 3** of my Cybersecurity & Ethical Hacking internship with
NetworkWalks Academy (Batch B083). Week 3 is all about **password cracking** — recovering
the passwords of encrypted PDF files and confirming the results by opening them. It has
two parts, each using a different toolset for the same goal:

- **Module 1 — Password Cracking with JTR:** using **John the Ripper (JTR)** and its graphical
  front-end **Johnny** — the industry-standard cracking tools.
- **Module 2 — Password Cracking with NetworkWalks Tools:** using NetworkWalks' own free,
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

## Module 1 · Password Cracking with John the Ripper (JTR)

**John the Ripper (JTR)** is the industry-standard password cracker; **Johnny** is its
point-and-click GUI. The goal of this module was to recover the passwords of three locked
practice PDFs and open them to confirm.

### Tools
- **John the Ripper (jumbo)** — command-line cracker
- **Johnny** — JTR graphical front-end
- **Online PDF Hash Extractor** — https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php

### Steps

**1. Set up and verify John (CLI)**
Install snap version of JTR CLI.

**2. Open Johnny (GUI)** — Johnny runs John underneath, so it's pointed at a valid John
executable and reports the detected version.

Johnny detects John the Ripper 1.9.0-jumbo — ready for attacks.

**3. Extract the PDF password hash** — upload each locked PDF to the online extractor. The
output **must start with `$pdf$`** (remove any `b'` prefix). Save each to its own file
(`hash1.txt`, `hash2.txt`, `hash3.txt`).

- https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php

The locked PDF converted to its <code>$pdf$</code> hash.</i></p>

**4. Crack the hashes** — done in Johnny (*Open password file → Start new attack*).

PDF 1 cracked → <b>password1</b>

PDF 2 cracked → <b>password1</b>

PDF 3 cracked → <b>1qaz2wsx</b>

**5. Verify — open the unlocked PDFs.** Each recovered password opened its PDF; PDF 3
revealed the flag.

All three PDFs unlocked with their recovered passwords.

### Results — PM1

| PDF file            | Recovered password | Why it was weak                  |
|---------------------|--------------------|----------------------------------|
| My Locked PDF1.pdf  | `password1`        | one of the most common passwords |
| My Locked PDF2.pdf  | `password1`        | one of the most common passwords |
| My Locked PDF3.pdf  | `1qaz2wsx`         | keyboard-walk pattern            |


<img width="646" height="389" alt="Screenshotl" src="https://github.com/user-attachments/assets/c00fbe09-9abe-4d8c-a259-22eac55fd1dd" />


<img width="953" height="410" alt="screenshot1" src="https://github.com/user-attachments/assets/3fdd0201-b9f9-49f1-a682-460a48256e50" />


<img width="919" height="388" alt="screenshot2" src="https://github.com/user-attachments/assets/9c713432-835f-4e00-ae8c-b529ad6af1a2" />


<img width="644" height="395" alt="screenshot3" src="https://github.com/user-attachments/assets/117dd328-dcf1-426a-9660-dd5e0b79fb53" />


<img width="945" height="378" alt="screenshot4" src="https://github.com/user-attachments/assets/b51e544d-2d00-4b8c-8df4-29be6ffae0c0" />


<img width="911" height="385" alt="screenshot5" src="https://github.com/user-attachments/assets/b08c9650-7a25-4ebb-b176-0801f146c836" />


<img width="638" height="392" alt="screenshot6" src="https://github.com/user-attachments/assets/d8fa4e20-0cbf-4d5c-a4bc-03379a61f264" />


<img width="958" height="391" alt="screenshot7" src="https://github.com/user-attachments/assets/ad552add-962d-480c-b23e-f16d69fd6ec3" />


<img width="943" height="395" alt="screenshot8" src="https://github.com/user-attachments/assets/a0a6de29-9746-4cf1-a828-b96422769cc8" />



---

## Module 2· Password Cracking with NetworkWalks Online Tools

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

PM2 lab task — password cracking with NetworkWalks online tools.

**2. Extract the hash** — in the Hash Calculator, open the **PDF** tab and upload the locked
PDF. It detects the encryption and outputs the `$pdf$` hash (Revision R4, Version V4,
128-bit key).

Hash Calculator extracts the <code>$pdf$</code> hash from the locked PDF

**3. Run the dictionary attack** — paste the hash into the Password Cracker and start it.
It tries each word in the built-in wordlist until it finds a match.

Dictionary attack matches the password 

**4. Verify — open the unlocked PDF** with the recovered password to reveal the flag.

PDF unlocked with password

---

### Results — PM2

| PDF file           | Recovered password | Method                         |
|--------------------|--------------------|--------------------------------|
| My Locked PDF1.pdf | `password1`        | dictionary attack (built-in wordlist) |
| My Locked PDF2.pdf | `password1`        | dictionary attack (built-in wordlist) |
| My Locked PDF1.pdf | `1qaz2wsx`        | dictionary attack (built-in wordlist) |



<img width="925" height="393" alt="screenshot9" src="https://github.com/user-attachments/assets/f4c08380-24a2-4558-bcba-318d545dcff7" />


<img width="932" height="390" alt="screenshot10" src="https://github.com/user-attachments/assets/4d4defa6-949a-47b8-8ffb-5a40aeacf4ad" />


<img width="917" height="389" alt="screenshot11" src="https://github.com/user-attachments/assets/5024b3f5-9ec1-4775-a6f0-8e571520f1dc" />


<img width="904" height="338" alt="screenshot12" src="https://github.com/user-attachments/assets/c6b35fcf-9b19-47e2-84ee-81fd51e65af2" />


<img width="803" height="398" alt="screenshot13" src="https://github.com/user-attachments/assets/768b82e9-f181-4e78-93ab-b22882edd87c" />


<img width="949" height="396" alt="screenshot14" src="https://github.com/user-attachments/assets/a063e9b6-f377-4faf-b4bc-0cfc5e7d896a" />


<img width="900" height="401" alt="screenshot15" src="https://github.com/user-attachments/assets/8ff49b8c-ad88-4f75-abaf-63c56acdd0dc" />


<img width="932" height="346" alt="screenshot16" src="https://github.com/user-attachments/assets/69e078a0-b5f2-43c9-8dc4-851051639e4f" />


<img width="930" height="396" alt="screenshot17" src="https://github.com/user-attachments/assets/4903310e-9fe2-45cc-b1e0-e5f1c77884fc" />


---

### Author

Priya Kishore Gehani | Networkwalks - Cybersecurity | Week 3 | B083
