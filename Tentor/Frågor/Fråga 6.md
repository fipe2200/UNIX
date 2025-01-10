# 2024-01-08
![[Pasted image 20250104115735.png]]
**Install MTA**: Set up Postfix for sending emails.

**Install MDA**: Configure Dovecot for receiving emails.

**Set up DNS records**:
- MX for mail server.
- SPF, DKIM for email validation.

**Secure the server**:
- Use TLS for encryption.
- Set up authentication (e.g., SASL).

**Test the server**:
- Send and receive emails.
- Check logs for errors.
---
# 2024-06-05
![[Pasted image 20250104115757.png]]

Related:
[[Fråga 4#SAMBA]]

---
# 2024-08-27
![[Pasted image 20250104115813.png]]
**SPF (Sender Policy Framework):**

*Purpose:
- Prevent email spoofing by verifying the sender's email address.
- *How it works:
- The domain owner specifies authorized mail servers in a DNS record (SPF TXT record).
- When a receiving mail server gets an email, it checks the SPF record to verify if the sending IP is authorized.
- If the IP is not listed, the email can be flagged as spam or rejected.

**DKIM (DomainKeys Identified Mail):**

- *Purpose:* 
- Ensure the integrity and authenticity of email content by using cryptographic signatures.
- *How it works:*
- The sending server adds a digital signature to the email header using a private key.
- The public key is published as a DNS TXT record.
- The recipient server uses the public key to verify the signature and confirm the email has not been altered.


# 2018-01-16
![[Pasted image 20250109135004.png]]
Samma som [[Fråga 5#2024-01-08]]
# 2018-03-21
![[Pasted image 20250109135023.png]]
**Types of attacks firewalls can prevent:
- Unauthorized access (e.g., blocking suspicious IP addresses).
- DDoS (to some extent, via rate-limiting rules).
- Port scanning and brute force attacks (e.g., restricting access to ports).

**Types of attacks firewalls can't detect:
- Internal threats from authenticated users.
- Encrypted malicious traffic (e.g., malware in HTTPS traffic).
- Application-layer attacks (e.g., SQL injection).
# 2018-10-30
![[Pasted image 20250109135052.png]]
![[Pasted image 20250110112715.png]]