# Cryptography Notes-basic

## What is Cryptography?

**Cryptography**: Practice and study of techniques for secure communication and data protection
- Confidentiality and integrity
- Authenticity 

**Cipher text** → encrypted plain text

**Cipher** → algorithm or method used to convert plaintext into ciphertext and back again into plain text

## Types of Encryption

Encryption is of two major types:
- **Symmetric** 
- **Asymmetric**

### Symmetric Encryption
Uses the same key to encrypt and decrypt data 
- Requires secure and safe transmission of key 
- Common examples are DES, 3DES, AES - these are standard encryption methods

### Asymmetric Encryption
Uses a pair of keys:
- One to encrypt the plain text or data
- One to decrypt the data back to plain text 

Also called **public key cryptography**
- Common examples are RSA, ECC, Diffie-Hellman 
- Tough to reverse without key 

## Use of Cryptography in Real World

- When you log in to TryHackMe, your credentials are encrypted and sent to the server so that no one can retrieve them by snooping on your connection.
- When you connect over SSH, your SSH client and the server establish an encrypted tunnel so no one can eavesdrop on your session.
- When you conduct online banking, your browser checks the remote server's certificate to confirm that you are communicating with your bank's server and not an attacker's.
- When you download a file, how do you check if it was downloaded correctly? Cryptography provides a solution through hash functions to confirm that your file is identical to the original one.

## Classic Encryption Methods

There are several types of encryption methods, but for what I started till now is classic encryption formats. But this is nowadays not that secure, hence there are several modern encryption styles which we will cover later. For now, classic encryptions are:

### Substitution Encryption
- Caesar cipher
- Monoalphabetic cipher
- Playfair cipher
- Hill cipher
- Polyalphabetic cipher
- One-time pad 

### Transportation Encryption
- Rail fence cipher
- Columnar transposition
- Route cipher

So first I will be covering the algorithm behind all these encryption classics, then I will be covering a room from TryHackMe Cryptography Basics.

---

## Substitution Encryption

### 1. Caesar Cipher
The most common and easy to crack encryption and also most basic, This involves setting a shift value.

**Example:**
- Taking plain text as input like `A`
- Setting shift value `3`
- So as our plain text is `A`, after encryption the alphabet will shift right by 3, so the output encrypted code will be `D`

Similarly, we set shift value and then traverse each and every alphabet of plain text and shift them by certain value to convert them into encrypted output.

**Note:** Easy and not secure (can be solved using brute force approach)

### 2. Monoalphabetic Cipher

It refers to a certain encryption format that uses modulo the number of characters in alphabet or whatever language you are using to convert it into encrypted form.

It is of 4 types:

**Variables:**
- `C`: encrypted cipher
- `K`: key 
- `P`: character plain text

#### a) Additive Cipher
`C = (P + K) mod 26` ⟹ formula used for encryption

#### b) Caesar Cipher  
Same as additive cipher, just it has a fixed value for key `K = 3`

`C = (P + 3) mod 26` ⟹ formula used for encryption

#### c) Multiplication Cipher 
`C = (P * K) mod 26` ⟹ formula used 

#### d) Affine Cipher
It is a combination of both multiplicative and additive cipher and also involves two keys:

`C = (P * K1 + K2) mod 26`

Where:
- `K1` ⟹ multiplicative key 
- `K2` ⟹ addition key 

### 3. Playfair Cipher

**Steps:**
1. Generate the key square (5×5) → unique 25 alphabets arranged in 5×5 format (usually J omitted in the matrix) (and if have to use J then J ↔ I replaced)
2. Plaintext is split into pairs of two letters. If odd number, Z is added to the last

### 4. Hill Cipher

**Process:**
Input → multiplied by n×n matrix (key) → modulo 26 → output (encrypt)

After multiplying with key matrix, an integer value is found. After that modulo 26 is done and the output is converted back into alphabet and returned as encrypted output.

### 5. Polyalphabetic Cipher

**Steps:**
1. Key preparation (to match the length of plain text)
2. Use a table like Vigenère square
<img width="480" height="480" alt="image" src="https://github.com/user-attachments/assets/a37022fc-5e0d-4244-ad22-546eccce0b5b" />

3. Find row corresponding to plain text letter
4. Find column corresponding to key letter
5. Intersection of row and column is the encrypted letter ⟹ cipher text letter 

### 6. One-Time Pad

**Process:**
1. **Key generation:** Random letters of same length as plain text
2. Each character of plain text is paired with key 
3. Both converted into numerical value (e.g., A=0, B=1)
4. Add both: plain text + key 
5. Modulo size of alphabet is taken - for English alphabet modulo 26 is taken 
6. After modulo, number is converted back to alphabet value 
7. All the letters are added to form an encrypted code 

---

## Transportation Encryption

### 1. Rail Fence Cipher (Zigzag Cipher)

**Process:**
- Number of rails is decided
- Based upon that, the plain text is written in a zigzag format 
- Then level-wise the values are noted, which forms the final encrypted code 

**Example with 3 rails:**
```
Plain text: "HELLO WORLD"
Rail 1: H   O   R
Rail 2:  E L   W O L
Rail 3:   L     D

Reading level-wise: HOR + ELWOL + LD = "HORELWOLLD"
```

### 2. Columnar Transposition

**Process:**
1. Choose a keyword (this determines the number of columns)
2. Write the keyword above the columns
3. Number the columns based on alphabetical order of keyword letters
4. Write the plaintext row by row under the columns
5. Read the ciphertext column by column in the order of the numbers

**Example:**
```
Keyword: "ZEBRA" → columns numbered as 5,2,1,4,3
Plain text: "HELLO WORLD"

Z E B R A
5 2 1 4 3
H E L L O
W O R L D

Reading in order 1,2,3,4,5: LR + EO + OD + LL + HW = "LREOODLLHW"
```

### 3. Route Cipher

**Process:**
1. Write the plaintext in a grid (rectangle or square)
2. Choose a specific route/path to read the text
3. Follow that route to create the ciphertext

**Common routes:**
- Spiral (clockwise/counterclockwise)
- Diagonal
- Alternating rows
- Column-wise reading

**Example (Spiral route):**
```
Plain text: "ATTACK AT DAWN"
Grid:
A T T A
C K A T
D A W N

Spiral route (clockwise from top-left): 
A→T→T→A→T→N→W→A→D→C→K→A = "ATTATNWADC KA"
```

