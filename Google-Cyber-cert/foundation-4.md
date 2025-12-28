# Basic Security Concepts

### Risk
- **Definition:** Anything that can impact the confidentiality, integrity, or availability of an asset
- Basically, it's the potential for something bad to happen to your important stuff

### Threat
- **Definition:** Any circumstance or event that can negatively impact an asset
- Think of it as the actual "bad thing" that could happen
- Examples: hackers, malware, natural disasters, human error

### Vulnerability
- **Definition:** A weakness that can be exploited by a threat
- It's like a hole in your defense that threats can take advantage of
- Could be outdated software, weak passwords, unpatched systems, etc.

**How they connect:**
- Vulnerability + Threat = Risk
- If there's no vulnerability, the threat can't really hurt you

---

## Cloud Based Services

### SaaS (Software as a Service)
- Software delivered over the internet
- You don't own it, you just use it
- Examples: Gmail, Google Docs, Dropbox, Netflix
- Everything managed by the provider

### PaaS (Platform as a Service)
- Gives you a platform to build and deploy apps
- You manage the applications and data
- Provider manages everything else (servers, storage, networking)
- Examples: Google App Engine, Heroku, AWS Elastic Beanstalk

### IaaS (Infrastructure as a Service)
- You rent the infrastructure (servers, storage, network)
- You have the most control here
- You manage OS, applications, data
- Examples: AWS EC2, Microsoft Azure, Google Compute Engine

**Quick way to remember:**
- **SaaS** = Use the software (least control)
- **PaaS** = Build on the platform (medium control)
- **IaaS** = Rent the hardware (most control)

---

## Principle of Least Privilege (PoLP)

- **Basic idea:** Users should only get the minimum level of access and authorization they need to do their job
- Don't give everyone admin rights!
- Reduces risk if an account gets compromised
- Example: A customer service rep doesn't need access to payroll data

**Why it matters:**
- Limits damage from insider threats
- Reduces impact of compromised accounts
- Makes it harder for attackers to move laterally in a system

---

## Data Governance

### Data Owner
- Usually a senior person (like a manager or executive)
- Decides who can access the data
- Responsible for the data's security and proper use
- Makes the rules

### Data Custodian
- The IT person/team who actually manages the data
- Implements the security controls
- Does backups, encryption, access control
- Follows the owner's rules

### Data Steward
- Ensures data quality and proper usage
- Makes sure data is accurate, complete, and used correctly
- Bridge between technical team and business side
- Focuses on data governance policies

**Simple analogy:**
- **Owner** = The boss who owns the car
- **Custodian** = The mechanic who maintains it
- **Steward** = The person who makes sure it's used properly

---

## Privacy Regulations

### GDPR (General Data Protection Regulation)
- European Union regulation
- Protects personal data of EU citizens
- Gives people rights over their data (right to be forgotten, etc.)
- Heavy fines for violations (up to 4% of annual revenue!)

### PCI DSS (Payment Card Industry Data Security Standard)
- For anyone who processes credit card payments
- Set of security standards to protect cardholder data
- Required if you handle credit card info
- Includes things like encryption, access control, monitoring

### HIPAA (Health Insurance Portability and Accountability Act)
- US regulation for healthcare data
- Protects patient health information (PHI)
- Strict rules about who can access medical records
- Penalties for breaches

---

## Cryptography Basics

### Hashing
- One-way function (can't be reversed)
- Always produces same output for same input
- Used for passwords, data integrity
- Examples: MD5 (weak), SHA-256 (strong)
- **Important:** Hash ≠ Encryption (you can't decrypt a hash!)

### Encryption & Decryption

#### Symmetric Encryption
- **Same key** for both encryption and decryption
- Faster but key distribution is tricky
- Examples: AES, DES, 3DES
- Problem: How do you securely share the key?

#### Asymmetric Encryption
- Uses **two keys:** public key and private key
- Public key encrypts, private key decrypts (or vice versa)
- Slower but solves key distribution problem
- Examples: RSA, ECC
- Used in: SSL/TLS, digital signatures, PGP

**Quick comparison:**
| Feature | Symmetric | Asymmetric |
|---------|-----------|------------|
| Keys | 1 (shared) | 2 (public + private) |
| Speed | Fast | Slower |
| Use case | Bulk data | Key exchange, signatures |

---

## Access Control - AAA Framework

### Authentication
- **"Who are you?"**
- Proving your identity
- Methods:
  - Something you know (password)
  - Something you have (token, phone)
  - Something you are (fingerprint, face)

### Authorization
- **"What are you allowed to do?"**
- Determining what resources you can access
- Happens AFTER authentication
- Based on roles, permissions, policies

### Accounting
- **"What did you do?"**
- Tracking and logging user activities
- Audit trails
- Important for compliance and security investigations

**Flow:** Authentication → Authorization → Accounting

---

## Additional Security Measures

### Single Sign-On (SSO)
- Log in once, access multiple applications
- More convenient for users
- Reduces password fatigue
- Examples: Login with Google, Microsoft, Facebook
- **Risk:** If SSO account is compromised, everything is compromised

### Multi-Factor Authentication (MFA)
- Requires 2 or more verification methods
- Combines different factor types:
  - Something you know (password)
  - Something you have (phone, token)
  - Something you are (biometric)
- **Much more secure** than just passwords
- Example: Password + SMS code, Password + authenticator app

**Best practice:** Use MFA whenever possible, especially for important accounts!

---

## Key Takeaways
- Security is layered (defense in depth)
- Always follow least privilege
- Encrypt sensitive data
- Use MFA wherever you can
- Know your regulations and stay compliant
- Document everything (accounting/logging)
