# Cert.se CTF 2023

Cert.se have hidden 7 flags provided in a zip file. In the zip file there is a Pcap file and a odt file

1. When opening the ODT file there is a word puzzle CTF[☔-ra+💿d=i+⛺t=d]
Symbols are Rain, CD and Tent converted to: 
CTF[Incident]

2. When ODT is converted to zip its possible to extract the meta data and the images of the file. In the meta.xml file there is line of code <meta:user-defined meta:name="CTF">CTF[WILLIAM]</meta:user-defined>
CTF[WILLIAM]

3. Using the tool https://stegonline.georgeom.net/upload its possible to use the function Inverse half and a flag is revealed:
https://github.com/tg222eu/CertCTF2023/blob/main/Solution/3.png
CTF[Sneaky]

4. I found the original picture of the second image on an online webshop. Comparing them there seem to be only 25 byte difference. When looking at the HexEditor at the bottom of the page E and e has been added. This looked like binary code and when converted to binary then to ASCI we get:
CTF[Bluffcity]

00000001 -> 1
00000000 -> 0
01000011 -> 67 ('C' in ASCII)
00000000 -> 0
01010100 -> 84 ('T' in ASCII)
00000000 -> 0
01000110 -> 70 ('F' in ASCII)
00000000 -> 0
01011011 -> 91 ('[' in ASCII)
00000000 -> 0
01000010 -> 66 ('B' in ASCII)
00000000 -> 0
01101100 -> 108 ('l' in ASCII)
00000000 -> 0
01110101 -> 117 ('u' in ASCII)
00000000 -> 0
01100110 -> 102 ('f' in ASCII)
00000000 -> 0
01100110 -> 102 ('f' in ASCII)
00000000 -> 0
01000011 -> 67 ('C' in ASCII)
00000000 -> 0
01101001 -> 105 ('i' in ASCII)
00000000 -> 0
01110100 -> 116 ('t' in ASCII)
00000000 -> 0
01111001 -> 121 ('y' in ASCII)
00000000 -> 0
01011101 -> 93 (']' in ASCII)

5. In the IRC chat there is a convertsation between Alice and Bob where BOB ask Alice to unlock the secret vault. Investigating futher from Bobs IP address he access a FTP server. A FTP-DATA protocol from this server reveals the flag:
CTF[Hunter2]
It can also be revealed by searching for "frame contains "CTF" or look directly at FTP-Data protocol in Protocol Hierarchy as its the only packet of its kind

6. By using binwalk I could see there are additional file inside the PCAP file. Extracting the files and opening up second file a private key and a certificate is revealed. When inserting the key in Edit -> Preference -> Protocol -> TLS -> RSA key list
Adding IP 192.168.0.10, Port: 443, Protocol HTTP, *Path to key*, a new HTTP protocol from the secret-management server is revealed with secret.png file. Extracting the HTTP object and open the picture reveal the flag:
CTF[GALOIS]
