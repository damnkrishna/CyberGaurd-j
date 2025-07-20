# Introduction to Networking 

networking refers to the way or method followed by world for transferring data and information from one place to another safely and accurately without leakage so there is several models followed for doing that

- OSI Model
- TCP/Ip Model

## OSI Model: 

Basic theory behind computer networking used for beginner to explain networking easily and by dividing parts so one can understand each layer role individually so there is total 7 layers 

### Application: 
interface used to transmit data using programmes running on computer, FTP protocol communication

### Presentation: 
data encryption convert the data into standardized format 

### Session: 
checks for link from sending and receiving computer if link established then keep it connected and separately so that data wont be mixed with multiple sessions and if not possible link send back error 

### Transport:
divides the message into small bits-sized pieces 
this also have two parts
- **TCP (Transmission control protocol)** = accuracy favoured over speed (eg. message, file transfer, webpage)
	- tcp -> segments
- **UDP ( User Datagram Protocol)** = speed is more important eg. video streaming
	- udp -> datagrams

### Networks:
responsible for locating the destination of your request and choose the best path/route to reach/transfer data to destination machine or ip

### Data Link:
receives packets using NIC or MAC address and verify for corruption or leak in packets while transmission before sending forward 

### Physical: 
covert the transmitted signal into binary data and binary to signals layer 1 of transmission 

## TCP/IP Model

this is a more old and more ideal model used actually in the whole world and as it doesn't have much sub layers it only got 4 layers so it is usually not preferred for explaining to beginner but it is the ideal model that is used in networking an have been used from a very long time actually

- similar to osi model or should i say osi model is similar to tcp/ip model that is more accurate
- 4 layers:
  - Application
  - Transport
  - Internet
  - Network Interface 

so tcp/ip protocol is not just a model name it is a set of rules that help in establishing a safe and secure transmission between two machines client and server 

so tcp/ip protocol involves 3 way handshake that helps in keeping data secure by only successfully connecting when whole three way communication is completed successfully 

- **TCP**: connection-based
- **UDP**: connection-less

so before any data is transmitted it has to follow tcp/ip protocol the famous three way handshake 

### Three-way Handshake

When you attempt to make a connection, your computer first sends a special request to the remote server indicating that it wants to initialise a connection. This request contains something called a SYN (short for synchronise) bit, which essentially makes first contact in starting the connection process. The server will then respond with a packet containing the SYN bit, as well as another "acknowledgement" bit, called ACK. Finally, your computer will send a packet that contains the ACK bit by itself, confirming that the connection has been setup successfully. With the three-way handshake successfully completed, data can be reliably transmitted between the two computers. Any data that is lost or corrupted on transmission is re-sent, thus leading to a connection which appears to be lossless.

## Encapsulation

process of wrapping data with necessary protocol information before transmission over a network 
 
its like placing a letter inside an envelope, then placing that enevelope inside a bigger one and again into a bigger envelope 

- each layer adds information needed for delivery 

this also enables reliable communication 

similary as once we encapsulat the data for transmission we also need to undo it or decrypt it so that we can get the data read it when reached the required destination machine or ip 

so this process is called de-encapsulation

so this process is not some model it is a method used to keep these model more secure by adding one more layer of security on it 

- observed in tcp/ip model
- observed in osi model

## Networking Tools

there is several tools present that is used for networking but in this blog I will be covering only the basic tool 
so there are 4 basic tool that tell a lot about networking data that can be used later on while hacking them or anything u are doing to them 

### PING
to test whether connection to a resource is possible or not does  it allow connection or not 

```bash
ping <target>                    # basic syntax
ping -4 <target>                 # tell only ipv4 address and stuff
ping -6 <target>                 # tell only ipv6 address and stuff
ping -I <time> <target>          # change the time interval for sending request to the target for checking for connections
```

I knew about ping and I actually used it sometime but I never knew that it is used for networking and for checking if connection was possible or not

### traceroute
so if u think when u search a website like facebook.com u directly open it but no that is not what happens in reality for reaching a specific website u go to several website before going to your target website that is commonly observed too while performing web pentesting so to keep the track of what website we are hopping before reaching our target a tool is present that Is used 

```bash
traceroute <target>              # basic syntax 
```

for Linux: traceroute
for windows: tracert

### whois
to find all the details about a web domain registration about company and domain and the info even they didn't know is visible about the time place expiration and stuff about someone domain and company 

```bash
whois <domain>                   # basic syntax
```

### dig
this tool is used for something related to dns server but I don't know much about them 

```bash
dig <domain> @<dns-server-ip>
```

so I knew about tcp/ip protocol but also got to know about the importance of tcp/ip model and osi model that is used for theory nowadays and learn some stuff I think this is enough for basic of networking 
next I will be posting more when studying about real tools that are very powerful and more used for networking like wireshark
