# 01 - Crack the Hash
## A hacker leaked the below hash online.Can you crack it to know the password of the CEO? 1ab566b9fa5c0297295743e7c2a6ec27

* Use https://hashes.com/en/tools/hash_identifier to identify the type of the hash (md5)
* Use https://hashes.com/en/decrypt/hash to decrypt the hash.

### flag: Iamtheflag


# 02 - RSA101
## we received a message from our agent but we don't know how to use our key to read the message Link: https://hubchallenges.s3-eu-west-1.amazonaws.com/crypto/RSA101.zip

* After downloading and unzipping the zip file, there will be 2 files the cipher text and the key, using the key decrypt the cipher text and find the contents of the file.
```
openssl pkeyutl -decrypt -in cipher -out decrypted -inkey key.pem 
cat decrtypted

```
### flag: flag{RSA_nice_try}

# 03 - Guess The Password
## A hacker leaked the below hash online.Can you crack it to know the password of the CEO? the flag is the password Hash: 06f8aa28b9237866e3e289f18ade19e1736d809d

* Use https://hashes.com/en/tools/hash_identifier to identify the type of the hash (sha1)
* Use https://hashes.com/en/decrypt/hash to decrypt the hash

### flag: jrahyn+

# 04 - Postbase
## We got this letters and numbers and don't understand them. Can you? R[corrupted]BR3tCNDUzXzYxWDdZXzRSfQ==

* the == at the end gives us a hint that it's base-64 encoding, so we use the command base64 --decode to decode it, but first we need to figure out the corrupted letters.
* The python script can help us in finding it (found online):
```python
#!/usr/bin/env python
import sys
import base64

str_base64 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"

for a in str_base64:
    for b in str_base64:
        try:
            str_flag = base64.b64decode("R" + a + b + "BR3tCNDUzXzYxWDdZXzRSfQ==")
            if ("flag" in str_flag) or ("FLAG" in str_flag):
                print "Found: {}".format(str_flag)
                sys.exit(0)
        except:
            continue
```

# 05 - Hide Data
## I used to hide my data with a classic cypher, can you get the flag hidden inside? 
## gur synt vf 2w68lsudym Vg vf cerggl rnfl gb frr gur synt ohg pna lbh frr vg v gbbx arneyl 1 zvahgr gb rapbqr guvf jvgu EBG13 tbbq yhpx va fbyivat gung

* There are mostly only letters so it's safe to assume it's some type of additive/shift cipher, 
* using https://www.dcode.fr/cipher-identifier we know the it's ROT-13 and using
* decode using https://www.dcode.fr/rot-13-cipher

output: the flag is 2j68yfhqlz It is pretty easy to see the flag but can you see it i took nearly 1 minute to encode this with ROT13 good luck in solving that

### flag: 2j68yfhqlz
