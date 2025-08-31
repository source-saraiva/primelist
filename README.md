# 🛡️ Primelist

Curated hosts and IP blocklists for use in DNS blockers, firewalls, and proxies.  
Primelist is maintained through aggregation of trusted sources and contributions from our own infrastructure (including hosts running Fail2Ban, which automatically submit abusive IPs).

---

### 📌 List Structure  

#### 🔹 Stable Lists (Default)  
These are the **curated and production-ready lists**, safe for daily use.  

- **`primelist_domains`**  
  Main domain blocklist containing advertising, tracking, and malware domains.  
  Aggregated from StevenBlack/hosts and other trusted sources, plus our contribution with additional curation and validation by our team.  
  Optimised for stability, with minimal false positives.

- **`primelist_badactors`**  
  IP blocklist of known malicious hosts (SSH brute-force, scanners, abuse sources).  
  Updated regularly with submissions from Fail2Ban-enabled hosts and abuse reports.  
  Intended for firewalls and intrusion prevention systems.  

#### 🔹 Evaluation / Experimental Lists  
Lists **under testing or aggregation**. They may contain duplicates or unverified entries and are **not recommended for production**.  

- **`primelist_domains_eval`**  
  Aggregated list (StevenBlack/hosts + internal candidates).  
  Entries are staged here before validation and promotion to `primelist_domains`.  

- **`primelist_badactors_eval`**  
  IPs collected from logs, Fail2Ban submissions, and abuse reports.  
  Candidates remain here until reviewed and promoted to `primelist_badactors`.  

---

### 📊 Promotion Flow  

Evaluation / Experimental        --->    Stable (Default)  
`primelist_domains_eval`         --->    `primelist_domains`  
`primelist_badactors_eval`       --->    `primelist_badactors`  

---
### ⚙️ How to Use the Lists  

Depending on your environment, you can integrate Primelist in several ways:  

#### 🔹 Pi-hole / AdGuard Home (DNS Blockers)  
- Add the raw list URL directly under **Blocklists**:
```bash
https://raw.githubusercontent.com/source-saraiva/primelist/refs/heads/main/primelist_domains.txt
```
- The domains will be blocked at DNS level.  
- Use `primelist_domains.txt` for stable blocking
#### 🔹 Hosts File (Workstations or Servers)  
- Download the file and append its contents to `/etc/hosts`. Make sure to install curl first if it is not already installed.
```bash
curl -s https://raw.githubusercontent.com/source-saraiva/primelist/refs/heads/main/primelist_domains.txt \
  | sudo tee -a /etc/hosts > /dev/null
 ```
- Flush DNS cache after updating (if needed).


---
### 🤝 How to Contribute  

We welcome contributions to make Primelist stronger and more reliable.  
There are three main ways to contribute:  

1. **Submit an Issue**  
   - If you find a false positive or want to suggest a new domain/IP, open an [issue on GitHub](../../issues).  
   - Please provide details (domain/IP, category, evidence if available).  

2. **Use our Public DNS Resolver**  
   - By using our resolver, you help us passively detect abusive domains through real-world traffic analysis.  
   - Public DNS details will be published soon.  

3. **Report via Fail2Ban Integration**  
   - If you run a server protected by Fail2Ban, you can configure it to automatically report banned IPs back to Primelist.  
   - This helps us keep the `primelist_badactors` list fresh and relevant.  
   - Configuration guide will be available in the [docs](docs/).  

---

### 🚀 Join Us  

Primelist is built with the community — by sysadmins, developers, and users like you.  
🛡️ **Together, we can maintain a cleaner, safer internet. Contribute today!**
