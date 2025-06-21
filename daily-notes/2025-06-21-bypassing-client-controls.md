# Bypassing Client-Side Controls

## Understanding Client-Server Communication

The client and server maintain constant communication. When a user sends input to a web application, it forwards that input to the server, and the server responds accordingly. This communication between client and server is often the main source of vulnerabilities in web applications.

## Common Client-Side Vulnerabilities

### Hidden Form Fields

Have you ever wondered if it's possible to change the price of goods online by manipulating the website and editing the price to your advantage? It's actually possible in some cases.

When ordering or buying items online, applications often provide a quantity field where users can input values. The application then calculates and displays the total price. However, developers sometimes leave vulnerabilities open by directly exposing price calculations to client-side manipulation.

**The Problem:**
- When users input quantity data, they may inadvertently expose price information
- If exploited by professionals, this could allow purchasing goods at reduced prices
- This poses significant problems for online companies, especially smaller businesses

**Potential Solution:**
Initially, you might think switching from text input to dropdown menus would solve this issue. However, **this approach is not secure either**. Switching from text input or hidden fields to dropdowns may reduce casual tampering, but it doesn't prevent determined attackers from manipulating requests.

**Important Note:**
Some applications have been found to accept negative prices, resulting in attackers receiving both a refund and the ordered goods. However, manipulating prices is illegal and unethical - it falls under black hat activities and should never be attempted.

### HTTP Cookies

This vulnerability was commonly abused in earlier times when developers trusted users too much, giving them access to modify cookies. Many users weren't even aware of this capability.

**Example Scenario:**
When someone logs into a shopping website and selects items to purchase, they might receive cookies like:

```
HTTP/1.1 302 Found
Location: /home.asp
Set-Cookie: SessId=191041-1042
Set-Cookie: UID=1042
Set-Cookie: DiscountAgreed=25
```

The third cookie (`DiscountAgreed=25`) presents a significant vulnerability. Users could potentially modify the discount value from 25 to 99 or 100, and the change might go unnoticed since it's part of the client-server communication.

### URL Parameters

Users can modify URL parameters to potentially access unauthorized functionality or data.

### The Referer Header

The Referer header can be manipulated to potentially gain direct access to internal application areas, bypassing normal navigation flows.

### Opaque Data

Some developers attempt to hide sensitive information (like prices) using encryption or encoding. However, this approach has several vulnerabilities:

- **Server-side decryption:** If prices are encrypted client-side but decrypted server-side, injection attacks might be possible
- **Token substitution:** Encrypted price tokens from cheaper items could potentially be copied and used for expensive items
- **Multiple attack vectors:** Various other methods exist to exploit these implementations

## Advanced Concepts

### ASP.NET ViewState

Modern developers have become more aware of security issues and often avoid direct client-server communication. Instead, they may use intermediary hosting solutions that communicate with users while protecting the main server.

However, attackers have also evolved their techniques. They may attempt to compromise hash codes or exploit the hosting layer to gain unauthorized access.

**Important:** While hosting servers in secure environments helps, real protection comes from proper logic, validation, and access control - not just relying on cloud hosting or obfuscation.

## Client Data Capture Methods

### HTML Forms

**Length Limitations:**
Developers often set input length limits believing this prevents injection attacks. However, these client-side restrictions can be bypassed, allowing various types of injection attacks.

**Disabled Elements:**
Form elements that appear fixed or unchangeable in the UI can still present vulnerabilities. These static elements may be susceptible to SQL injection, cross-site scripting, and other attacks if not properly secured server-side.

### Thick Client Components

Besides HTML forms, applications may use thick-client components for data capture and validation:

- Java applets
- ActiveX controls  
- Shockwave Flash objects

These components can potentially be reverse-engineered to understand the application's source code and identify vulnerabilities.

## Security Best Practices

### Handling Client-Side Data Security

**Critical Principle:** Client-side controls (JavaScript validation, hidden inputs, UI restrictions) are **not real security measures**. Skilled attackers can easily modify or bypass these controls.

**Key Takeaway:** All meaningful validation and security checks must be implemented and enforced on the server side. Client-side controls should only be used for user experience improvements, never as security measures.

## Conclusion

Understanding these vulnerabilities is crucial for web developers and security professionals. The key principle is that anything happening on the client side can be manipulated by users. True security must always be implemented and enforced on the server side, with proper validation, authentication, and authorization mechanisms.

**Ethical Note:** This information is provided for educational purposes to help developers build more secure applications. Any attempt to exploit these vulnerabilities for malicious purposes is illegal and unethical.
