
## Challenge Overview  
  
We are given a packet capture file `half-awake.pcap`. The challenge description hints that some packets are pretending to be something they are not, suggesting we should carefully inspect protocol data rather than trusting protocol labels.  

## Initial Analysis  
  
Opening the `.pcap` file in Wireshark, most traffic appears to be normal client chatter. However, one packet containing an **HTTP 200 OK response** includes the following text:  

Read this slowly:

1. mDNS names are hints: alert.chunk, chef.decode, key.version
2. Not every 'TCP blob' is really what it pretends to be
3. If you find a payload that starts with PK, treat it as a file

These instructions provide several hints:  
  
- Look at **mDNS records** for clues.  
- Some TCP payloads may contain **hidden data**.  
- Data beginning with **PK** should be treated as a **ZIP file**.  
  
---  
  
## Identifying the Hidden File  
  
Searching through the packets revealed an **Encrypted Alert** packet containing the following bytes:  
50 4b 03 04

These hex values correspond to the **magic number of a ZIP archive** (`PK`).  
  
Examining the packet payload confirms that it contains ZIP file structures including filenames such as:  

stage2.bin  
readme.txt

## Extracting the ZIP Archive  
  
The relevant packet bytes were copied starting from the `PK` signature and saved as a `.zip` file.  
  
After extracting the archive we obtain two files:  

stage2.bin  
readme.txt

Contents of `readme.txt`:  

not everything here is encrypted the same way

The `stage2.bin` file contains non-readable binary data:  

u�f�a�{�4�f�a�4�3�s�3�t�3�p�0�0�0�_�r�c�}

This suggests the file is encoded or encrypted.  

## Finding the Key  
  
The HTTP message earlier referenced **mDNS hints**, including:  

key.version

Inspecting the **mDNS records in Wireshark** reveals a value for the key version:  

00b7

This suggests that the data may be encoded using **XOR with key 00b7**.  
  
---  
  
## Decoding the Payload  
  
To decode the file:  
  
1. Take the hex stream of `stage2.bin`  
2. Open CyberChef  
3. Apply the following steps:  
   - `From Hex`  
   - `XOR` with key `00b7`  
  
![CyberChef decoding process](../../Screenshots/half-awake-cyberchef.png)  
  
---  
  ![[half-awake-cyberchef.png]]
## Flag  

utflag{h4lf_aw4k3_s33_th3_pr0t0c0l_tr1ck}