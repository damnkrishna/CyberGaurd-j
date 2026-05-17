# have to start log analysis again 

there are several layrs in osi model and several protection rule as for data layer 
there is aloha => pure aloha
               => slotted aloha
then there is csma and csma/cd 

both are used for data protection 


two of the most important hashing technique used are 
DES 
RSA
both are industry grade encryption alogrithums

SELECT * FROM users WHERE username = 'admin' OR '1'='1' AND password = '...';
    ```
    *(The `OR '1'='1'` condition evaluates to true, bypassing authentication entirely).*
*   **Mitigation:** Use **Parameterized Queries / Prepared Statements** (separates code from data), input validation, and the Principle of Least Privilege for database accounts.

### Cross-Site Scripting (XSS)
Occurs when an application includes untrusted data in a web page without proper validation or escaping, allowing malicious client-side scripts (usually JavaScript) to execute in the victim's browser.

*   **Stored (Persistent) XSS:** The malicious script is permanently stored on the target server (e.g., in a database, comment section) and served to every user visiting the page.
*   **Reflected (Non-Persistent) XSS:** The script is part of a malicious URL or request parameter and is immediately reflected back by the server onto the response page.
*   **DOM-Based XSS:** The vulnerability exists entirely in client-side JavaScript processing; the payload is executed by modifying the DOM directly in the browser.
*   **Mitigation:** Context-aware **Output Encoding** (HTML, JavaScript, CSS encoding), enforcing a strong **Content Security Policy (CSP)**, and setting `HttpOnly` flags on session cookies.

---

## 3. Cryptography & Mathematical Foundations

### Principles of Computer Security (CIA Triad & Beyond)
*   **Confidentiality:** Ensuring data is accessible only to authorized entities (achieved via Encryption).
*   **Integrity:** Assuring the accuracy and trustworthiness of data over its lifecycle (achieved via Hashing/MACs).
*   **Availability:** Ensuring reliable access to information by authorized users (defended via redundant systems, DDoS mitigation).
*   **Non-Repudiation:** Preventing an entity from denying an action or transaction (achieved via Digital Signatures).

### Data Encryption Standard (DES)
A legacy symmetric block cipher that processes 64-bit blocks of plaintext using a 56-bit key length (with 8 parity bits making up a 64-bit total key).
*   **Structure:** Uses a **Feistel Network** structure over 16 rounds.
*   **Weakness:** The 56-bit key space ($2^{56}$ combinations) is highly vulnerable to modern brute-force attacks.

### RSA (Rivest-Shamir-Adleman)
The foundational asymmetric (public-key) cryptosystem used for secure key exchange and digital signatures. Its security relies on the hardness of **prime factorization**.

#### Mathematical Algorithm:
1. Choose two large distinct prime numbers, $p$ and $q$.
2. Compute the modulus $n = p \times q$.
3. Compute Euler's totient function: $\phi(n) = (p-1)(q-1)$.
4. Choose an integer $e$ (public exponent) such that $1 < e < \phi(n)$ and $\gcd(e, \phi(n)) = 1$.
5. Calculate the private exponent $d$ such that:
$$d \equiv e^{-1} \pmod{\phi(n)} \quad \text{or} \quad (d \times e) \pmod{\phi(n)} = 1$$
6. **Keys:** Public Key = $(e, n)$, Private Key = $(d, n)$.
7. **Encryption:** $C = M^e \pmod n$
8. **Decryption:** $M = C^d \pmod n$

### Hashing
A cryptographic hash function maps input data of arbitrary size to a fixed-size bit string (a message digest) in a strictly one-way deterministic operation.

#### Key Properties:
*   **Pre-image Resistance (One-Way):** Given a hash $H$, it is computationally infeasible to find the original input $x$ such that $Hash(x) = H$.
*   **Second Pre-image Resistance:** Given an input $x_1$, it is infeasible to find a different input $x_2$ such that $Hash(x_1) = Hash(x_2)$.
*   **Collision Resistance:** It is computationally infeasible to find *any* two distinct inputs $x_1$ and $x_2$ such that $Hash(x_1) = Hash(x_2)$.
*   **Avalanche Effect:** A tiny change in the input (e.g., changing one bit) drastically alters the resulting output hash.

---

## 4. System & Advanced Security Topics

*Depending on the specific textbook alignment of your course, these modules typically drill into:*
*   **Endpoint & OS Security:** Memory protection mechanisms like Address Space Layout Randomization (**ASLR**), Data Execution Prevention (**DEP** / NX bit), and protecting against buffer overflow attacks.
*   **Intrusion Detection/Prevention Systems (IDS/IPS):** **Signature-based detection** (matching known bad patterns/hashes) vs. **Anomaly-based detection** (building a baseline of normal network behavior and flagging deviations using heuristics or machine learning).
*   **Authentication & Access Control:** Implementing Role-Based Access Control (**RBAC**), Attribute-Based Access Control (**ABAC**), and secure protocols like OAuth 2.0, OIDC, and multi-factor authentication (MFA).

---
ing the mathematical steps of **RSA**, write out a mockup of a parameterized vs unparameterized SQL statement, and trace how a packet flows during a **DNS Amplification** attack to secure the highest-yielding points on the exam.
