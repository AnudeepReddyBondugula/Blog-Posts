---
title: "Identity Management in ISE"
datePublished: Tue Jul 29 2025 17:06:45 GMT+0000 (Coordinated Universal Time)
cuid: cmdoshbbt000302kz3bdvbl0h
slug: identity-management-in-ise
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753808742399/a744019f-af76-4030-a379-7aa536eee4c3.webp
tags: security, identity-management, ccnp-security, identity-services-engine

---

Welcome to the **CCNP Security Series**. In this post, we’ll talk about **Identity Management** and **Identity Stores**

# What is an Identity?

In network security, **identity** simply answers the question: “Who are you?”

It might be your name, a username, or even the MAC address of a device. But just saying “I’m Alex” or “This is a printer” isn’t enough—**you need to prove it.**

That’s where **credentials** come in. Credentials are trusted evidence used to **verify** an identity. Think of them like a digital passport:

* For people: usernames, passwords, smart cards, certificates
    
* For devices: MAC addresses, machine certificates
    

These credentials help systems like **Cisco ISE** identify and verify users or devices before giving access to the network.

In simple terms:

* Identity = Who you are
    
* Credential = Proof of who you are
    

# Identity Stores in Cisco ISE

So now that we know what an identity is, the next question is:  
**Where is this identity stored and verified?**

That’s the role of an **identity store**—a database that contains user or device credentials.

Cisco ISE uses these stores to **authenticate** and **authorize** identities.

There are two types of identity stores:

## Internal Identity Stores

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9780136677710/files/graphics/02fig01.jpg align="left")

Cisco ISE comes with its **own internal user database**. This is useful for:

* Temporary accounts (e.g., contractors, guests)
    
* Admin accounts for managing network devices
    
* Lab or test environments
    

You can create these accounts directly within ISE and organize them into **identity groups** like “Employees” or “Guests.”

## External Identity Stores

Most organizations rely on **external** identity sources that ISE can integrate with, such as:

* **Active Directory (AD)**
    
* **LDAP servers**
    
* **Certificate Authorities**
    
* **One-Time Password (OTP) servers**
    
* **Smart card systems**
    
* **SAML Identity Providers (IdPs)**
    

These external stores are scalable and centralized, making them ideal for production use.

# Whats Next?

Now that you understand how identities and identity stores work in Cisco ISE, it’s time to learn **how those identities actually get authenticated on the network.**

In the next post, we’ll cover: **Extensible Authentication Protocol (EAP) over LAN: 802.1X**

You’ll learn how EAP works, why it matters, and how 802.1X enables secure identity-based access to the network.

Stay tuned!

---

🛠 *This blog is part of the "CCNP Security ISE Theory" series. Follow along as we break down each concept clearly and simply.*