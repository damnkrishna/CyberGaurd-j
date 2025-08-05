# Attacking Access Controls

Access controls are a critical defense mechanism for application security. There are two types of access controls:

- **Vertical** => Accessing higher level roles/controls like admin only stuff
- **Horizontal** => Ensures users only access their own resources and not others

When a user can view or modify resources to which they are not entitled to, this represents a security vulnerability.

Sometimes horizontal separation of privileges can lead directly to vertical escalation attacks.

## Identifier-Based Functions

Some websites have URL links for admin only content or confidential documents that can be opened only through URL links shared to specific persons or higher officials. However, these URL links don't have any authentication or protection, so if guessed or leaked by some ex-employee, it can be a big problem for the security of the website.

**Reason:**
- When the main application is interfacing to an external system or back-end component
- Session-based security model is tough for developers to install, so they take shortcuts into client-submitted parameters

## Multistage Functions

I've observed some developers don't involve authentication at each page - they assume that if someone has reached a certain page, they must have been through verification at an earlier stage.

## Static Files

Sometimes files like annual reports and stuff are shared directly from the server with no authentication and no protection. Anyone with the link can access all data and modify the URL to find other data.

## Mapping Exercise Before Attacking Access Controls

- Discover hidden content and public information
- Leverage web server using Nikto, Nmap
- Analyze the application pages and functionality
- Identify entry points for user input
- Map the attack surface

**If Found:** Application segregates user access to different levels of functionality and different resources (e.g., documents)

**To Do:** Use two different level accounts, find certain functions or documents that can't be accessed/shown in one account, and try to access it through the other account.

## Securing Access Controls

- Do not rely on application URLs or document links => authorized access only
- Do not trust any user-submitted parameters (admin=true)
- Do not assume users will access application pages in intended sequence
- Do not let users tamper with any data using request/response

## Best Practices for Access Controls

### Define Access Rules Clearly
Document who can access each function and what data they can use.

### Use Session-Based Decisions
Base access control on the user's authenticated session.

### Centralize Access Control
Implement a single component to handle all access checks.

### Validate Every Request
Route all client requests through this central component to enforce access rules.

### Enforce Access Checks in Code
Require all pages to explicitly define access control logic.

### Add IP Restrictions for Sensitive Areas
For admin pages, restrict access to specific IP ranges for extra security.

### Protect Static Files
- Use a server-side script to serve files only after access checks
- Or use HTTP authentication/server features to control direct file access

### Validate Client-Side Identifiers
- Any resource IDs sent from the client (e.g., in URLs or forms) are vulnerable to tampering
- Always revalidate them on the server to ensure the user has proper access

### Secure Critical Actions
For sensitive operations (e.g., adding bank payees), implement:
- Per-transaction reauthentication
- Dual authorization

This protects against misuse, even if the session is hijacked.

### Enable Logging
- Log every access to sensitive data or performance of sensitive actions
- Helps in detecting and investigating access control breaches

## Use a Multi-Layer Privilege Model

A multi-layer privilege model provides defense in depth by implementing multiple levels of access control. This approach ensures that if one layer fails, other layers can still protect the system.

### Programmatic Control
Code-level access controls that are embedded directly in the application logic. These controls are enforced at runtime and can make dynamic decisions based on user context, request parameters, and business logic.

### Discretionary Access Control (DAC)
A model where access rights are granted at the discretion of the resource owner. The owner can decide who gets access to their resources and what level of access they receive. This is commonly seen in file systems where users can set permissions on their own files.

### Role-Based Access Control (RBAC)
Access permissions are assigned to roles rather than individual users. Users are then assigned to appropriate roles based on their job functions. This simplifies management as permissions are managed at the role level rather than for each individual user.

### Declarative Control
Access control rules are defined externally from the application code, typically in configuration files, databases, or policy engines. This separation allows for easier management and modification of access rules without changing the application code.

By implementing multiple layers, you create a robust security posture where each layer provides additional protection and can compensate for weaknesses in other layers.
