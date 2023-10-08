## Forensics
* Forensics is the art of recovering the digital trail left on a computer.



### File Format
* File Extensions are not the sole way to identify the type of a file, files have certain leading bytes called file signatures which allow programs to parse the data in a consistent manner.
* Files can also contain additional "hidden" data called metadata which can be useful in finding out information about the context of a file's data.

#### File Signatures
* File signatures (also known as File Magic Numbers) are bytes within a file used to identify the format of the file.
* Generally they’re 2-4 bytes long, found at the beginning of a file.
* Files can sometimes come without an extension, or with incorrect ones. We use file signature analysis to identify the format (file type) of the file. Programs need to know the file type in order to open it properly.

##### How do you find the file signature?
* You need to be able to look at the binary data that constitutes the file you’re examining. To do this, you’ll use a hexadecimal editor. (hexdump FILENAME)
* Once you find the file signature, you can check it against file signature repositories such as Gary Kessler’s (https://www.garykessler.net/library/file_sigs.html)

#### Tools
hexdump (Terminal: hexdump FILENAME)




### Metadata
* Metadata is data about data.
* Different types of files have different metadata.
* EXIF Data is metadata attached to photos which can include location, time, and device information.

#### Timestamps
* Timestamps are data that indicate the time of certain events (MAC): - Modification – when a file was modified - Access – when a file or entries were read or accessed - Creation – when files or entries were created
* Certain events such as creating, moving, copying, opening, editing, etc. might affect the MAC times. If the MAC timestamps can be attained, a timeline of events could be created.
  
##### Timestamps Types
* Modified
* Accessed
* Created
* Date Changed (MFT)
* Filename Date Created (MFT)
* Filename Date Modified (MFT)
* Filename Date Accessed (MFT)
* INDX Entry Date Created
* INDX Entry Date Modified
* INDX Entry Date Accessed
* INDX Entry Date Changed

##### Patterns
* ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/0b521357-c94f-44fd-8ca5-e2a9968b169a)
* ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/3a655263-02b8-451a-842f-be7409d972b7)
* ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/5e6783eb-4552-4f28-9fb6-4d2e9b3646c9)
* ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/d23558d8-2c93-44e6-91a8-684dcb79ef00)
* ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/ce3393d7-4c19-4785-94ce-21ee79544ff5)

#### Tools
* AccessData FTK Imager (Installed on Windows)
* Exif tool (Terminal: exiftool FILENAME)



### Wireshark and PCAPs
* Wireshark is a network protocol analyzer which is often used in CTF challenges to look at recorded network traffic.
* Wireshark uses a file type called PCAP to record traffic.
* The network traffic displayed initially shows the packets in order of which they were captured.
* You can filter packets by protocol, source IP address, destination IP address, length, etc.
* Filters can be chained together using '&&' notation.
* The most pertinent part of a packet is its data payload and protocol information.

#### Decrypting SSL Traffic
* By default, Wireshark cannot decrypt SSL traffic on your device unless you grant it specific certificates.

##### High-Level SSL Handshake Overview
* In order for a network session to be encrypted properly, the client and server must share a common secret for which they can use to encrypt and decrypt data without someone in the middle being able to guess.
* Handshake loosely follows this format:
  1. The client sends a list of available cipher suites it can use along with a random set of bytes referred to as client_random
  2. The server sends back the cipher suite that will be used, such as TLS_DHE_RSA_WITH_AES_128_CBC_SHA, along with a random set of bytes referred to as server_random
  3. The client generates a pre-master secret, encrypts it, then sends it to the server.
  4. The server and client then generate a common master secret using the selected cipher suite
  5. The client and server begin communicating using this common secret

##### Decryption Requirements
* If you have the client and server random values and the pre-master secret, the master secret can be generated and used to decrypt the traffic
* If you have the master secret, traffic can be decrypted easily
* If the cipher-suite uses RSA, you can factor n in the key in order to break the encryption on the encrypted pre-master secret and generate the master secret with the client and server randoms 



### Steganography
* Stegonagraphy is the practice of hiding data in plain sight.
* Stegonagraphy is often embedded in images or audio.

#### LSB Steganography
* Files are made of bytes. Each byte is composed of eight bits.
* Changing the least-significant bit (LSB) doesn’t change the value very much.
* So we can modify the LSB without changing the file noticeably. By doing so, we can hide a message inside.

##### LSB Steganography in Images
* Say an image has a pixel with an RGB value of (255, 255, 255)
* By modifying the lowest, or least significant, bit, we can use the 1-bit space across every RGB value for every pixel to construct a message.
* The reason steganography is hard to detect by sight is because a 1-bit difference in color is insignificant.
* Decoding LSB steganography is exactly the same as encoding, but in reverse. For each byte, grab the LSB and add it to your decoded message. Once you’ve gone through each byte, convert all the LSBs you grabbed into text or a file. (You can use your file signature knowledge here!)

#### Tools
* Online websites



### Disk Imaging
* A forensic image is an electronic copy of a drive (e.g. a hard drive, USB, etc.). It’s a bit-by-­bit or bitstream file that’s an exact, unaltered copy of the media being duplicated.
* Wikipedia said that the most straight­forward disk imaging method is to read a disk from start to finish and write the data to a forensics image format.
* To prevent write access to the disk, you can use a write blocker.
* It’s also common to calculate a cryptographic hash of the entire disk when imaging it. “Commonly-used cryptographic hashes are MD5, SHA1 and/or SHA256,”.
* By recalculating the integrity hash at a later time, one can determine if the data in the disk image has been changed.
* This by itself provides no protection against intentional tampering, but it can indicate that the data was altered.

#### Tools
* AccessData FTK Imager (Installed on Windows)

### Memory Forensics
* Some of the most valuable information can be found within memory dumps, that is images taken of RAM.



#### Volatility Basics
* A good workflow is as follows:
  1. Run strings for clues
  2. Identify the image profile (which OS, version, etc.)
  3. Dump processes and look for suspicious processes
  4. Dump data related interesting processes
  5. View data in a format relating to the process (Word: docx, Notepad: txt, Photoshop: psd, etc.)

##### Profile Identification
* In order to properly use Volatility you must supply a profile with --profile=PROFILE, therefore before any sleuthing, you need to determine the profile using imageinfo:
* python3 vol.py -f FILEPATH imageinfo

##### Dump Processes 
* In order to view processes, the pslist or pstree or psscan command can be used.
* python vol.py -f FILEPATH --profile=PROFILE pstree

##### Process Memory Dump
* Dumping the memory of a process can prove to be fruitful, say we want to dump the data from a process with the id 2019
* vol.py -f FILEPATH --profile=PROFILE memdump -p 2019 -D PATHTODUMP

##### Other Useful Commands
*Other Useful Commands
* python3 vol.py -f IMAGE --profile=PROFILE connections (view network connections)
* python3 vol.py -f IMAGE --profile=PROFILE cmdscan (view commands that were run in cmd prompt)
