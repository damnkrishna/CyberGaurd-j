# Attacking Session Management 

Sessions play a crucial role in any web application as they enable applications to uniquely identify a user across different requests like admin user, etc. Also, they are the prime target for malicious attacks to bypass authentication and access admin controls by using and modifying tokens issued by web applications.

Sessions are used for:
- Login pages
- Online shopping platforms
- Banking stuff

Vulnerabilities:
- Weak session tokens generation
- Weak handling of session tokens

Alternative to sessions:
- HTTP authentication
- Sessionless state mechanisms
  - If token issued is fairly long (100 or more bytes)

## Weakness in Session Tokens 

Session tokens are usually encoded using:
- XOR 
- Base64
- Hexadecimal

These can be decrypted/decoded for private info like username, email, password, date, role, etc.

### Predictable Tokens
Observed usually in e-commerce and official websites that use several tokens daily, so one can learn and understand these session tokens and decrypt and use them for their own goal or gaining admin role or stuff.

### Concealed Sequence 
Contains sequence that reveal themselves when the tokens are suitably decoded or unpacked:
- Have to understand pattern 
- Try different pattern
- Decode them
- Use for your use

### Time dependency
Session tokens that are generated based on timestamps or time patterns can be predicted by analyzing the timing of token creation and finding correlations with system time.

### Weak random number generation 
Poor random number generators or pseudorandom functions make session tokens predictable, allowing attackers to guess or calculate future token values based on observed patterns.

### Full blown tests for randomness
Session tokens should be tested for true randomness using statistical tests to ensure they cannot be predicted or have detectable patterns that attackers can exploit.

## Weakness in Session Token Handling 

Hijacking of session is possible if one just knows the token - no need to decrypt it. You just need to replace it with normal user token and you are in as admin.

- Disclosure of tokens on Network
