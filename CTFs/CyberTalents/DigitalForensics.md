## 01 G&P List

* Given a file, run binwalk to know the content of the binary file (binwalk FILENAME)
* Using binwalk you will find that it's a zipped file 
* Unzip the file and you will find the flag.txt (unzip FILENAME)

#### flag: 877c1fa0445adaedc5365d9c139c5219


## 02 Hidden Message

* Given an image, run binwalk to know the content of the binary file (binwalk FILENAME)
* No extra files were found, run strings to know the hidden strings (strings FILENAME)
* No hidden strings were found, run xxd to know the hexadecimal contents (xxd FILENAME)
* The flag is in the hexadecimal contents

#### flag: b1a1f2855d2428930e0c9c4ce10500d5

## 03 Cypher Anxiety

* Given a zip file, unzip the file (unzip FILENAME)
* Try binwalk, nothing important is found (binwalk FILENAME) 
* check for hidden strings (strings FILENAME | head -n 100 (because the hidden strings were too many))
* Find the following text 

```
Hey bro
S\U	
Sup supp, are we ready
yeah, u got the files?
yes but i think the channel is not secured
the UTM will block the file transfer as the DLP module is active
ok we can use cryptcat
ok what the password then
let it be P@ssawordaya
hhh, ok
listen on 7070 and ill send you the file , bye
.....
```

* Open wireshark to analyze the packet 
* Since they are listening on port 7070 we will filter by that port (tcp.port == 7070)
* The PSH packets is the packets that have the data so focus on the PSH packets (The first PSH packet between 2 nodes is to agree about the the sequance nubmers so the First packet not have any data)
* To make it easier you can filter by PSH packets (tcp.port == 7070 && (tcp.flags.push == 1))
* Download the raw file of the first PSH packet (the second because the first one is to agree on the sequence as mentioned earlier)
* Use cryptcat to simulate the connection they did using the same password (cryptcat -l -k P@ssawordaya -p 1234 > N1_Output)
* Send the file to yourself on the encrypted channel (nc 127.0.0.1 1234 < FILENAME)
* After 5s end the connection and you will find the image
* The flag is the md5 of the image (md5sum FILENAME)

#### flag: 3beef06be834f3151309037dde4714ec

## 04 Partition Lost

* Given an image, use FTK Imager to access the files on the image
* Locate fl@4.rar zip file
* Try to unzip
* The file is corrupt
* Read the hexadecimal data using FTK Imager
* Find the flag in the hexadecimal data

#### flag: FLAG(701_L@b$_DR_DFIR)

## 05 Search in Trash
* Download the file
* Use file to know the type (file FILENAME)
* It's recycle bin info2 file 
* use rifiuti to scan the file (rifiuti2 FILENAME)
* You will find the flag in the information provided by rifituti2.

#### flag: FLag{Fat_32_DF_2}

* Alternatively, you can use strings to find the hidden strings and reach the same result (strings FILENAME)

## 06 Message in a Bottle (TBD)
Desperately, I tried openstego and got the following error:
I finally have you!
After trying an older version (v0.6.1), I got the flag Flag{701_L@b$_CTF0}. Honestly, I've learned now that always try to try tools first before going off the deep-end and over-analyzing. Breadth-first, over depth-first.
