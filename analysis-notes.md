# Wireshark Packet Analysis – Detailed Notes

This document explains all observations made while analyzing network traffic using **Wireshark** on my local test environment.  
The goal is to understand packet behaviour and identify normal vs suspicious traffic patterns.

---

# 1. Filters Used in This Analysis

These filters were used to isolate different types of packets:

tcp
dns
arp
http
icmp
tcp.flags.syn==1
tcp.flags.ack==1


Each filter helped focus on specific network events.

---

# 2. TCP 3-Way Handshake Analysis

TCP


### 🔹 What I observed
- **SYN** → Client requests connection  
- **SYN-ACK** → Server responds  
- **ACK** → Client confirms  

This completes the 3-way handshake.

### 🔹 Why it matters (Security POV)
- Too many SYN packets = possible **SYN Flood attack**  
- Repeated SYN → no ACK = **scanner activity**  
- Unusual port handshakes = suspicious connections  

---

# 3. DNS Query & Response Analysis

Filter used:

DNS


### 🔹 What I observed
- Client requested IP resolution for domain names  
- Server responded with A/AAAA records  
- Status codes were normal (“No Error”)

### 🔹 Security importance
- Continuous DNS lookups to strange domains = **malware beaconing**  
- Failed DNS queries repeatedly = suspicious network behaviour  

---

# 4. ARP Traffic Analysis

Filter used:

ARP


### 🔹 What I observed
- “Who has 192.168.x.x? Tell 192.168.x.x”
- ARP replies mapping IP → MAC

### 🔹 Security importance
- Unknown devices answering ARP = **ARP spoofing**  
- Too many ARP broadcasts = maybe a misconfigured host  

---

# 5. HTTP Traffic (if available)

Filter used:

HTTP


### 🔹 What I observed
- GET / POST requests  
- Cleartext URLs  
- Hostnames visible  
- Data exchanged without encryption  

### 🔹 Security notes
- HTTP traffic is readable → vulnerable  
- Sensitive data must NEVER be sent over HTTP  

---

# 6. Example Suspicious Patterns (Practice)

These are common red flags to watch for:

- Repeated SYN packets without completing handshake  
- DNS queries to random generated domains  
- ARP replies coming from unknown MAC addresses  
- Large ICMP packets (possible ping flood)  

---

# 7. Conclusion

This lab helped in:
- Understanding packet-level behaviour  
- Interpreting communication flow  
- Detecting anomalies  
- Gaining skills required for **SOC L1 analysis**

.


Filter used:
tcp
