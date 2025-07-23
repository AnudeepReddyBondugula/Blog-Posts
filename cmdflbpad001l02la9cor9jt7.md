---
title: "Fundamentals of AAA"
seoTitle: "AAA Basics Explained"
seoDescription: "Learn AAA (Authentication, Authorization, Accounting), TACACS+, and RADIUS for securing device administration and network access"
datePublished: Wed Jul 23 2025 06:36:31 GMT+0000 (Coordinated Universal Time)
cuid: cmdflbpad001l02la9cor9jt7
slug: fundamentals-of-aaa
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753252159009/8be47b0d-754f-4b25-9ddb-b08c54329edf.png
tags: authentication, security, authorization, accounting, radius, ccnp-security, tacacs

---

In this post, we’ll cover the basics of **AAA (Authentication, Authorization, Accounting)**.

### What is AAA?

* **Authentication** – Who are you? (e.g., login with username/password)
    
* **Authorization** – What are you allowed to do? (e.g., view or configure)
    
* **Accounting** – What did you do? (e.g., logs of commands or access)
    

---

## 🎛️ **Device Administration**

* Device administration AAA controls **who can log in** to a network device (console, Telnet, SSH) and **what commands they can run**.
    

## 🌐 **Network Access**

* Network access AAA is used to **verify the identity** of a user or device **before allowing them onto the network**.
    
* It ensures only trusted users/devices can connect and is commonly used in **802.1X, VPN, and Wi-Fi authentication**.
    

---

## TACACS+

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753242331610/8002c9de-12cc-4181-96dc-3721d90c1a41.png align="left")

**TACACS+** is a protocol used for **device administration** (e.g., logging into Cisco routers or switches). It uses **TCP port 49** and is commonly used with Cisco ISE as the AAA server.

### Why Use Tacacs+?

* Separates **Authentication**, **Authorization**, and **Accounting**
    
* Fully **encrypts** the packet body
    
* Supports **per-command authorization**, making it ideal for CLI sessions
    
* Used when managing access to devices like switches, routers, and firewalls
    

### Authentication Messages

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9780136677710/files/graphics/01fig04.jpg align="center")

3 message types used:

| **Message** | **Direction** | **Purpose** |
| --- | --- | --- |
| START | Client → Server | Initiates authentication |
| REPLY | Server → Client | Requests or responds (e.g., prompt for username) |
| CONTINUE | Client → Server | Sends user input (username, password, etc.) |

Final REPLY can be:

* `ACCEPT` – Auth successful
    
* `REJECT` – Auth failed
    
* `ERROR` – Something went wrong\`
    
* `CONTINUE` – More input needed
    

### Authorizaton Messages

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9780136677710/files/graphics/01fig05.jpg align="center")

| **Message** | **Purpose** |
| --- | --- |
| REQUEST | Client asks for access to a service/command |
| RESPONSE | Server replies with result (`PASS`, `FAIL`, etc.) |

Common RESPONSE types:

* `PASS_ADD`, `PASS_REPL`, `FAIL`, `FOLLOW`, `ERROR`
    

### Accounting Messages

| Message | Description |
| --- | --- |
| REQUEST | Reports activity (`START`, `STOP`, `CONTINUE`) |
| RESPONSE | Acknowledges (`SUCCESS`, `ERROR`, `FOLLOW`) |

---

## RADIUS

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9780136677710/files/graphics/01fig02.jpg align="left")

**RADIUS** is used especially for **network access control** like 802.1X, VPNs, and Wi-Fi.

It works on a **client/server model** and uses **UDP port 1812 (auth)** and **1813 (acct)**.

### Why Use RADIUS?

* Designed for **network access AAA**
    
* Transports **EAP** for 802.1X authentication
    
* Combines **authentication + authorization** in a single flow
    
* Used in wired, wireless, VPN, and remote access scenarios
    

### Authentication & Authorization Messages

| Message Type | Direction | Purpose |
| --- | --- | --- |
| Access-Request | Client → Server | Starts authentication; includes service type (e.g., 802.1X, MAB, etc.) |
| Access-Accept | Server → Client | Authentication success + authorization info (AV pairs: VLAN, dACL, etc.) |
| Access-Reject | Server → Client | Authentication failed |
| Access-Challenge | Server → Client | Requests more input (e.g., OTP) |

### Accounting Messages

| Message Type | Purpose |
| --- | --- |
| Accounting-Request | Sent by client; includes START/STOP info |
| Accounting-Response | Acknowledgment from server |

### Common Service-Type Values

| Value | Name | Use Case |
| --- | --- | --- |
| 1 | Login | Web auth (non-Cisco devices) |
| 2 | Framed | IEEE 802.1X |
| 5 | Outbound | Local web auth |
| 10 | Call-Check | MAC Authentication Bypass |

---

## Summary: RADIUS & TACACS+

| Feature | RADIUS | TACACS+ |
| --- | --- | --- |
| Used For | Network Access | Device Admin |
| Protocol | UDP | TCP |
| Port (default) | 1812/1813 | 49 |
| Auth & AuthZ Split | ❌ Combined | ✅ Separated |
| EAP Support | ✅ Yes | ❌ No |
| Encryption | Partial (password only) | Full body |

---

## AV Pairs

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9780136677710/files/graphics/01fig09.jpg align="left")

### What Are AV Pairs?

In RADIUS, responses are sent using **Attribute-Value pairs (AV pairs)**.

Each **attribute** describes something (like VLAN), and its **value** defines what to apply.

### Example AV Pairs:

| Attribute | Value |
| --- | --- |
| VLAN ID | 20 |
| Access Control List | ACL\_ALLOW |
| Session-Timeout | 1800 secs |

These AV pairs define **what a user can do after authentication**.

---

## Change of Authorization (CoA)

By default, RADIUS is **client-initiated** – meaning the AAA server can’t act unless the client starts a request.

But what if we want to **force a reauth**, **disconnect a session**, or **change access** mid-session?

That’s where **CoA** comes in.

### What CoA Can Do:

* Re-authenticate a user
    
* Disconnect a session
    
* Bounce a switch port (shut/no shut)
    
* Apply new policies dynamically
    

CoA is defined in:

* **RFC 3576** (initial)
    
* **RFC 5176** (updated)
    

### Why CoA Matters:

ISE uses **CoA extensively** to:

* Enforce policy changes
    
* Move users between VLANs
    
* Quarantine infected endpoints
    
* Trigger reauthentication based on posture
    

Without CoA, network access control would be **static** — CoA makes it **dynamic and policy-driven**.

## 📘 What's Next: Identity Management in Cisco ISE

Now that we’ve covered the fundamentals of AAA, RADIUS, and TACACS+, it's time to look at **Identity Management**.

In the next article, we’ll explore:

* What is an *identity* in ISE?
    
* Identity store options: **LDAP, AD, PKI, OTP, smart cards, local databases**
    
* Internal vs. external identity sources
    
* Identity store sequences
    
* How identities integrate with **ISE authentication policies**
    
* Using **X.509 certificates and PKI** in secure authentication
    

➡️ Stay tuned for the next post:  
**"Identity Management in Cisco ISE"**

---

🛠 *This blog is part of the "CCNP Security ISE Theory" series. Follow along as we break down each concept clearly and simply.*