# Nmap Complete Cheat Sheet (2026 Edition)

**Target:** Ethical hackers, red teamers, SOC analysts, penetration testers & cybersecurity professionals.  
**Usage:** Scan only networks you own or have explicit written permission for. Unauthorized scanning is illegal.

---

## 1. Basic Usage & Target Specification

| Command                          | Example                              | Description                              |
|----------------------------------|--------------------------------------|------------------------------------------|
| Single host/IP                   | `nmap 192.168.1.1`                   | Scan one IP or hostname                  |
| Multiple hosts                   | `nmap 192.168.1.1 10.0.0.1`          | Multiple IPs                            |
| CIDR range                       | `nmap 192.168.1.0/24`                | Subnet scan                              |
| IP range (dash)                  | `nmap 1.1.1.1-10`                    | Range scan                               |
| From file                        | `nmap -iL targets.txt`              | List of targets                         |
| Random hosts                     | `nmap -iR 100`                       | Random selection                         |
| Exclude hosts                    | `nmap --exclude 192.168.1.1 target`  | Skip specific hosts                      |
| Domain/hostname                  | `nmap scanme.nmap.org`              | Standard scanme site                     |

---

## 2. Scan Techniques (Most Used by Hackers & Experts)

| Flag     | Name                        | Description                                      | When to Use (Most Common)                     |
|----------|-----------------------------|--------------------------------------------------|-----------------------------------------------|
| -sS      | TCP SYN (Stealth)           | Half-open (default & fastest)                    | **Most popular** – stealthiest real-world scan |
| -sT      | TCP Connect                 | Full 3-way handshake                            | No root required or SYN blocked                |
| -sU      | UDP                         | UDP empty packets + ICMP error                   | UDP services (slow but essential)             |
| -sA      | TCP ACK                     | Firewall mapping                                 | Firewall analysis                             |
| -sW      | Window Scan                 | Window size checks                               | Advanced OS/firewall                          |
| -sM      | Maimon Scan                 | FIN/URG/PSH flags                                | Stealth evasion                                |

**Pro Tip:** Start every scan with `-sS` unless you need root or it fails.

---

## 3. Host Discovery (Before Port Scan)

| Flag          | Example                          | Description                              |
|---------------|----------------------------------|------------------------------------------|
| -sP / -sn     | `nmap -sn 192.168.1.0/24`        | Ping sweep only (no ports)              |
| -Pn           | `nmap -Pn target`                | Skip discovery (assume all up)          |
| -PS / -PA     | `nmap -PS22,80 target`           | SYN/ACK to specific ports               |
| -PU           | `nmap -PU53 target`              | UDP probe                               |
| -PE / -PP     | `nmap -PE target`                | ICMP echo / timestamp                   |
| -PR           | `nmap -PR localnet`              | ARP for local networks                  |

**Pro Tip:** `-sn` is the fastest way to map live hosts before a full scan.

---

## 4. Port Specification (Critical for Performance)

| Flag               | Example                              | Description                              |
|--------------------|--------------------------------------|------------------------------------------|
| All ports          | `-p-` or `-p1-65535`                 | Full port range                          |
| Top 1000 ports     | `--top-ports 1000`                   | **Most used by experts**                 |
| Fast common ports  | `-F`                                 | 100 common ports (fast)                  |
| Specific ports     | `-p 22,80,443,3389`                  | Custom list                               |
| Service names      | `-p http,https,ssh`                  | Named services                           |
| TCP + UDP mixed    | `-p U:53,T:22,80`                    | Mixed scan                                |

**Pro Tip:** `-p-` or `--top-ports 1000` is the default most hackers use first.

---

## 5. Aggressive Scanning (-A = Most Used by Experts)

| Command                    | Description                                      |
|----------------------------|--------------------------------------------------|
| `-A`                       | **Fastest & most complete** (OS + Version + Scripts + Traceroute) |
| `-A -T4`                   | Balanced (recommended for live tests)            |
| `-A -T5`                   | Maximum speed                                    |

---

## 6. NSE Scripts (The Real Power Tool)

| Command                              | Description                                      | Example                              |
|--------------------------------------|--------------------------------------------------|--------------------------------------|
| `-sC`                                | Default safe scripts                             | `nmap -sS -sC target`                |
| `--script vuln`                      | All vulnerability scripts                        | `nmap --script vuln target`          |
| `--script http-*`                    | HTTP enumeration                                 | `nmap -sV --script http-* target`    |
| `--script smb*`                      | SMB brute/enumeration                            | `nmap -sV --script smb* target`      |
| `--script http-sql-injection`        | SQLi checks                                      | `nmap --script http-sql-injection target` |
| `--script http-title`                | Page title grab                                  | `nmap -p80 --script http-title target` |

**Pro Tip:** Use `-sC` only on confirmed open ports for maximum stealth.

---

## 7. Stealth, Evasion & Advanced Flags

| Flag                  | Example                              | Description                              |
|-----------------------|--------------------------------------|------------------------------------------|
| `-f` / `--mtu 32`     | `nmap -sS -f target`                 | Fragment packets (harder to detect)     |
| `-D decoy1,target`    | `nmap -D 192.168.1.101,target target` | Decoy scan (masks your IP)              |
| `-S spoofed-IP`       | `nmap -S 10.0.0.100 target`          | Source IP spoofing                      |
| `-g 53`               | `nmap -g 53 target`                  | Source port 53 (very stealthy)          |
| `--data-length 200`   | `nmap -sS --data-length 200 target`  | Add random data to packets              |
| `-T0` to `-T5`        | `-T1` (Paranoid) or `-T4` (most used)| Timing & stealth levels                  |

**Stealth Example:** `nmap -sS -T1 -f -D decoy1,target target`

---

## 8. Service / Version & OS Detection

| Flag           | Description                                      |
|----------------|--------------------------------------------------|
| `-sV`          | Version detection (use with `-sS`)               |
| `-O`           | OS detection                                     |
| `-O --osscan-guess` | Aggressive guessing                           |

---

## 9. Timing & Performance Tuning

| Flag                     | Example                    | Description                              |
|--------------------------|----------------------------|------------------------------------------|
| `-T0` to `-T5`           | `-T4`                      | **Most used** – balanced speed/stealth   |
| `--min-rate 1000`        | `--min-rate 2000`          | Packets per second                       |
| `--max-rate 500`         | `--max-rate 500`           | Cap rate                                 |
| `--host-timeout 5m`      | `--host-timeout 2h`        | Give up on slow hosts                    |
| `--min-hostgroup 100`    | `--min-hostgroup 50`       | Parallelism control                      |

---

## 10. Output Formats

| Flag                  | Example                     | Description                              |
|-----------------------|-----------------------------|------------------------------------------|
| `-oN file.txt`        | `nmap -oN scanme.txt target`| Normal readable text                     |
| `-oX file.xml`        | `nmap -oX scanme.xml target`| XML (import into Ndiff, etc.)            |
| `-oA prefix`          | `nmap -oA scanme target`    | All formats at once                      |
| `-oG file`            | `nmap -oG scanme.gnmap`     | Grepable format                          |
| `-oG -`               | `nmap -oG -`                | Grepable to screen                       |
| `-v` / `-vv`          | `nmap -vv target`           | Verbose output                           |
| `--open`              | `nmap --open target`        | Only show open ports                     |

---

## 11. Most Common Daily Workflow (Real-World Commands)

1. **Fastest recon on one target**  
   `nmap -sS -sV -sC -A -T4 target`

2. **Quick host sweep**  
   `nmap -sn 192.168.1.0/24`

3. **Fastest common ports**  
   `nmap -T4 --top-ports 1000 target`

4. **UDP + aggressive**  
   `nmap -sU -A target`

5. **Evasion (live test)**  
   `nmap -sS -T1 -f -D decoy1,target target`

6. **Scripted vulnerability hunt**  
   `nmap -sV --script=vuln target`

**Pro Tip:** Start every new target with `-A -T4` – this is the #1 command used by 90% of experts.

---

## 12. Installation (Quick)

**Linux:** `sudo apt update && sudo apt install nmap`  
**macOS:** `brew install nmap`  
**Windows:** Download from [nmap.org](https://nmap.org/download.html)

---

## 13. Reading Output (Key Terms)

- **open** – Port is listening  
- **filtered** – Firewall blocking (no response)  
- **closed** – Port is closed  
- **open|filtered** – UDP common  
- **Running: Linux 6.x** – OS fingerprint  
- **OpenSSH 9.x** – Service version

---
