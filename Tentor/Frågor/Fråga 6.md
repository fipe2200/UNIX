# 2024-01-08
![[Pasted image 20250104115735.png]]

---
# 2024-06-05
![[Pasted image 20250104115757.png]]

---
# 2024-08-27
![[Pasted image 20250104115813.png]]
**SPF (Sender Policy Framework):**

- *Purpose:
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