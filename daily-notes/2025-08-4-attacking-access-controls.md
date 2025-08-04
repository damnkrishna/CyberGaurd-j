# Attacking Access Controls

Critical defense mechanism for application security. Two types of access controls:

**Vertical** => accessing higher level role/control like admin only stuff (prevents lower privileged users from accessing admin functions)

**Horizontal** => ensures user only access their own resource and not others (prevents users from accessing other users data at same privilege level)

When a user can view or modify resources to which he is not entitled to, sometimes horizontal separation of privileges can lead directly to vertical escalation attacks

## Identifier-Based functions

Some website have url link for admin only or some document that are confidential and can be opened only through url link that is shared only to specific person or higher official but these url link doesn't have any authentication or protection so if guessed or leaked by some ex-employee it can be a big problem for security of website 

Reason: 
- when main application is interfacing to an external system or back-end component 
- session based security model tough for developers to install so they take short way out into client submitted parameters
