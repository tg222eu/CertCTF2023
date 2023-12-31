# Cert.se CTF 2023

Cert.se have hidden 7 flags provided in a zip file. In the zip file there is a Pcap file and a odt file

1. When opening the ODT file there is a word puzzle CTF[☔-ra+💿d=i+⛺t=d]
Symbols are Rain, CD and Tent converted to: 
CTF[Incident] <br><br>

![alt text](https://github.com/tg222eu/CertCTF2023/blob/main/Solution/2.JPG)<br>
2. When ODT is converted to zip its possible to extract the meta data and the images of the file. In the meta.xml file there is line of code <meta:user-defined meta:name="CTF">CTF[WILLIAM]</meta:user-defined>
CTF[WILLIAM]<br><br>

![alt text](https://github.com/tg222eu/CertCTF2023/blob/main/Solution/3.png)<br>
3. Using the tool https://stegonline.georgeom.net/upload its possible to use the function Inverse half and a flag is revealed:
https://github.com/tg222eu/CertCTF2023/blob/main/Solution/3.png
CTF[Sneaky]<br><br>

![alt text](https://github.com/tg222eu/CertCTF2023/blob/main/Solution/5.JPG)<br>
4. I found the original picture of the second image on an online webshop. Comparing them there seem to be only 25 byte difference. When looking at the HexEditor at the bottom of the page E and e has been added. This looked like binary code and when converted to binary then to ASCI we get:
CTF[Bluffcity]

<details>
  <summary>Binary to ASCII</summary> <br>
  00000001 -> 1<br>
00000000 -> 0<br>
01000011 -> 67 ('C' in ASCII)<br>
00000000 -> 0<br>
01010100 -> 84 ('T' in ASCII)<br>
00000000 -> 0<br>
01000110 -> 70 ('F' in ASCII)<br>
00000000 -> 0<br>
01011011 -> 91 ('[' in ASCII)<br>
00000000 -> 0<br>
01000010 -> 66 ('B' in ASCII)<br>
00000000 -> 0<br>
01101100 -> 108 ('l' in ASCII)<br>
00000000 -> 0<br>
01110101 -> 117 ('u' in ASCII)<br>
00000000 -> 0<br>
01100110 -> 102 ('f' in ASCII)<br>
00000000 -> 0<br>
01100110 -> 102 ('f' in ASCII)<br>
00000000 -> 0<br>
01000011 -> 67 ('C' in ASCII)<br>
00000000 -> 0<br>
01101001 -> 105 ('i' in ASCII)<br>
00000000 -> 0<br>
01110100 -> 116 ('t' in ASCII)<br>
00000000 -> 0<br>
01111001 -> 121 ('y' in ASCII)<br>
00000000 -> 0<br>
01011101 -> 93 (']' in ASCII)
</details>

<br><br>
![alt text](https://github.com/tg222eu/CertCTF2023/blob/main/Solution/1.JPG)<br>
5. In the IRC chat there is a convertsation between Alice and Bob where BOB ask Alice to unlock the secret vault. Investigating futher from Bobs IP address he access a FTP server. A FTP-DATA protocol from this server reveals the flag:
CTF[Hunter2]
![alt text](https://github.com/tg222eu/CertCTF2023/blob/main/Solution/secret.png)<br>
It can also be revealed by searching for "frame contains "CTF" or look directly at FTP-Data protocol in Protocol Hierarchy as its the only packet of its kind
<br><br>
![alt text](https://github.com/tg222eu/CertCTF2023/blob/main/Solution/6.JPG)<br>
6. By using binwalk I could see there are additional file inside the PCAP file. Extracting the files and opening up second file a private key and a certificate is revealed. When inserting the key in Edit -> Preference -> Protocol -> TLS -> RSA key list
Adding IP 192.168.0.10, Port: 443, Protocol HTTP, *Path to key*, a new HTTP protocol from the secret-management server is revealed with secret.png file. Extracting the HTTP object and open the picture reveal the flag:
CTF[GALOIS]
<br><br>
![alt text](https://github.com/tg222eu/CertCTF2023/blob/main/Solution/signal.JPG)<br>
7. I was unable to find the last flag. I highly supect its in the message.wav file that was sent between Alice and Christina. I noticed there is a tone in the file. Because the song loops I took one part of the loop, inverted it, matched the section with the sound and put both to left channel. That way I filter out almost all music. When listening to it there is a coded beep signal. Its not morse code. The beeps have 7 different length. I measured out the signal accourding to their duration

1224122412241223213321333164122222162124312251621232218122231731224122412241
