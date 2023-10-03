# CTFs
https://overthewire.org/wargames/natas/

## Level 0

* Start by viewing the page source 
* Flag/Password is in the source

 ![image](https://github.com/Anas-Ehab/2023RoadmapNotes/assets/55194408/1c273bf8-1d91-46c8-91d2-97d1ad0c0fe0)


#### Flag/Password: g9D9cREhslqBKtcA2uocGHPfMZVzeFK6

## Level 1
* You can't right click so instead to view the page source use (view-source: URL)
* Flag/Password is in the source

![image](https://github.com/Anas-Ehab/2023RoadmapNotes/assets/55194408/a23aa8b6-70db-41a4-a6db-263995cbb862)

* You can also CTRL and then Right Click it will also work
#### Flag/Password: h4ubbcXrWqsTo7GGnnUMLppXbOogfBZ7

## Level 2
* Check the source of the page
* You will find a path to a file
  ![image](https://github.com/Anas-Ehab/2023RoadmapNotes/assets/55194408/f1920c0f-8b35-4691-a864-fd71bed667f0)

* Check the directory (URL/files/)
  ![image](https://github.com/Anas-Ehab/2023RoadmapNotes/assets/55194408/fd53e657-f986-4e73-b769-45ac2af333c7)

* You will find another file that contains the users infromation
  ![image](https://github.com/Anas-Ehab/2023RoadmapNotes/assets/55194408/f24a488b-be36-4bd8-aa70-07a6cccef2d8)

#### Flag/Password: G6ctbMJ5Nb4cbFwhpMPSvxGHhQ7I6W8Q


## Level 3
* Check for robots.txt (http://natas3.natas.labs.overthewire.org/robots.txt)
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/95f7ccec-ddd7-4a76-95ea-97600c759dc9)

* Check the mentioned directory (http://natas3.natas.labs.overthewire.org/s3cr3t/)
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/3791ff26-328e-48a6-9a4b-2154910d6b7a)

* Open the file and you will find the username and password
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/96a26994-3a37-4450-bde4-988c0f0f21bf)

#### Flag/Password: tKOcJIbzM4lTs8hbCmzn5Zr4434fGZQm

## Level 4
* By Pressing the refresh button and capturing the packet we can change the Referer to Natas5 using Burp
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/3ae9fb92-a312-4956-a4c0-bbdc11cb1249)

* After doing so we will get the password

  #### Flag/Password: Z0NsrtIkJoKALBCLi5eqFfcRN82Au2oD

## Level 5
* By capturing the packet of logging in we will see that there is a *Cookie: loggedin=0* line by changing the 0 to 1 using Burp we get access

#### Flag/Password: fOIvE0MDtPTgRhqmmvvAOt2EfXR6uQgR

## Level 6
* View the source of the page or press the view source button and you will find a file named: *index-source.html*
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/ab9b496d-884c-4e72-b43f-b336b5fd49d5)

* Check this file and you will find an included file which the password is taken from (*includes/secret.inc*)
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/276f9e8f-c2c3-4787-829b-a5f5529f4c40)

* Check this file and you will get the secret (*http://natas6.natas.labs.overthewire.org/includes/secret.inc*)
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/de08ce3c-bbc5-4458-bca5-652778810efc)

* Typing in the secret will give you the flag (*FOEIUWGHFEEUHOFUOIU*)
  
#### Flag/Password: jmxSiH3SP6Sonf8dv66ng8v1cIEdjXWr

## Level 7
* View the source of the page and you will find a hint *<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->*
  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/6e689744-ca2e-415f-a41b-6029dfa991d2)

  * By checking the URL you will find that the page is passed as a parameter to a function in index.php *index.php?page=home*
  
  * By changing the parameter to */etc/natas_webpass/natas8* you will get the flag (http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8)

#### Flag/Password: a6bZCNYwdKqN5cGP11ZdtPg0iImQQhAB

## Level 8
* View the source of the page and you will find the function that checks the secret

  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/0cbf2843-cbb1-426b-974e-51e38b694f2c)

  By examining this we can figure the way to reverse it, first we need to reverse the bin2hex by using hex2bin after that we take the output and we use strrev on it, finally we decode it from base64

* After doing all of this we get the secret which is: *oubWYf2kBq*
* By typing in the secret we get the flag

#### Flag/Password: Sda6t0vkOPkM8YeOZkAGVhFoaplvlJFd

## Level 9
* By examining the source code we find out that whatever we type is included with no filtering
* By testing file traversal we find it vulnerable (test;cat ../../../../etc/natas_webpass/natas10)
* The flag is shown in the file natas10

#### Flag/Password: D44EcsFkLxPIkAAKLosx8z3hxX1Z4MCE


## Level 10
* 

