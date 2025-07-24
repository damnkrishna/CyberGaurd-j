# Computer Fundamentals - Class Notes

## Why Computers Use Binary (Not Hexadecimal or Decimal)

Today I learned why computers don't use hexadecimal, decimal, or any other number system for storing memory and processing data internally. The fundamental reason is:

**Computers only understand two states: 0 or 1** (electric pulse present or not present)

This binary nature makes binary code the most natural low-level language for computers. Since computers can only distinguish between "yes" or "no" (on/off electrical states), binary is the perfect match for this limitation.

## Binary Number System

With binary codes, you can represent any number:
- 5 → 101 (in binary)
- 10 → 1010 (in binary)
- 255 → 11111111 (in binary)

Similarly, you can convert any decimal number into binary code representation.

## Binary Operations

All mathematical operations can be performed using binary:

### Basic Operations
- **Addition (A + B)**: Can be performed using binary arithmetic
- **Subtraction (A - B)**: Uses binary subtraction algorithms
- **Multiplication (A × B)**: Implemented through binary multiplication
- **Division (A ÷ B)**: Executed via binary division methods

The expressions and algorithms might change compared to decimal operations, but understanding these binary operations helps you:
- Understand computation at the ground level
- Create unique operations yourself
- Grasp how the computer actually processes data

**Key Insight**: This is why understanding the inner workings of computer systems is crucial for any computer science student.

## Computer Block Diagram

When we start up our computer or laptop, the following process occurs:

1. **Input Reception**: Various inputs are sent to the system
2. **Task Execution**: Based on these inputs, certain pre-defined tasks and new tasks start working
3. **CPU Processing**: All processing happens within the CPU

## CPU Components

The CPU (Central Processing Unit) consists of three main components:

### 1. Memory Unit
- Stores data and instructions temporarily
- Provides quick access to frequently used information
- Works closely with RAM and cache memory

### 2. ALU (Arithmetic Logic Unit)
- Performs all arithmetic operations (addition, subtraction, multiplication, division)
- Handles logical operations (AND, OR, NOT, XOR)
- Executes comparison operations

### 3. Control Unit
- Manages and coordinates all CPU operations
- Controls the flow of data between different components
- Interprets and executes instructions
- Synchronizes all computer operations

## Key Takeaways

- Binary is the foundation of all computer operations
- Understanding low-level operations helps in creating efficient programs
- The CPU's three-component architecture enables all computer functionality
- Memory unit plays a crucial role in data storage and retrieval

## Additional Notes

- **Hexadecimal**: While not used internally by computers, hex is often used by programmers as a convenient way to represent binary data (since each hex digit represents exactly 4 binary digits)
- **Performance**: Understanding these fundamentals helps in writing more efficient code and optimizing program performance
- **Hardware-Software Bridge**: This knowledge connects how software instructions translate to hardware operations

---

*Today's focus was primarily on the memory unit component and its role in computer operations.*
