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

4. I found the original picture of the second image. Comparing them there seem to be only 25 byte difference. When looking at the HexEditor at the bottom of the page E and e has been added. This looked like binary code and when converted to binary then to ASCI we get CTF[Bluffcity]

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

5. In the IRC chat there is a convertsation between Alice and Bob where BOB opens up a secret vault. Investigating futher from Bobs IP address he access a FTP server. A FTP-DATA protocol from this server reveals the flag:
CTF[Hunter2]
It can also be revealed by searching for "frame contains "CTF" or look directly at FTP-Data protocol in Protocol Hierarchy


******RSA******
Found certificate in packet 3422 and extracted it

Was able to looking at it in "openssl x509 -in cert -text -noout"
Extracted public key "openssl x509 -pub.key -noout -in cert > pub.key
python3 RsaCtfTool.py --publickey pub.key --private
Sorry, cracking failed.

*****Picture 2******

Found the original photo on the internet. A cmp indicate there is no difference between the original and the CTF file. Higly likely that there is no flag in this file

------foremost------

foremost -i picture.jpg: No hidden data in footer/header

---------Stegseek---------

stegseek --seed picture.wav

error: Could not find a valid seed.

--------Exiftool:-----------

ExifTool Version Number         : 12.40
File Name                       : 100000000000040000000300B296674118E1FCC5.jpg
Directory                       : .
File Size                       : 182 KiB
File Modification Date/Time     : 2023:10:04 16:35:30+02:00
File Access Date/Time           : 2023:10:04 16:40:25+02:00
File Inode Change Date/Time     : 2023:10:04 16:36:18+02:00
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Exif Byte Order                 : Little-endian (Intel, II)
Orientation                     : Horizontal (normal)
X Resolution                    : 96
Y Resolution                    : 96
Resolution Unit                 : inches
Y Cb Cr Positioning             : Centered
Exif Version                    : 0210
Components Configuration        : Y, Cb, Cr, -
Flashpix Version                : 0100
Color Space                     : Uncalibrated
Exif Image Width                : 1024
Exif Image Height               : 768
Profile CMM Type                : Little CMS
Profile Version                 : 2.1.0
Profile Class                   : Display Device Profile
Color Space Data                : RGB
Profile Connection Space        : XYZ
Profile Date Time               : 2012:01:25 03:41:57
Profile File Signature          : acsp
Primary Platform                : Apple Computer Inc.
CMM Flags                       : Not Embedded, Independent
Device Manufacturer             :
Device Model                    :
Device Attributes               : Reflective, Glossy, Positive, Color
Rendering Intent                : Perceptual
Connection Space Illuminant     : 0.9642 1 0.82491
Profile Creator                 : Little CMS
Profile ID                      : 0
Profile Description             : c2ci
Profile Copyright               : CC0
Media White Point               : 0.9642 1 0.82491
Red Matrix Column               : 0.43607 0.22249 0.01392
Green Matrix Column             : 0.38515 0.71687 0.09708
Blue Matrix Column              : 0.14307 0.06061 0.7141
Red Tone Reproduction Curve     : (Binary data 64 bytes, use -b option to extract)
Green Tone Reproduction Curve   : (Binary data 64 bytes, use -b option to extract)
Blue Tone Reproduction Curve    : (Binary data 64 bytes, use -b option to extract)
Image Width                     : 1024
Image Height                    : 768
Encoding Process                : Progressive DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 1024x768
Megapixels                      : 0.786

------------exiv2------------
File name       : 100000000000040000000300B296674118E1FCC5.jpg
File size       : 186065 Bytes
MIME type       : image/jpeg
Image size      : 1024 x 768
Thumbnail       : None
Camera make     :
Camera model    :
Image timestamp :
File number     :
Exposure time   :
Aperture        :
Exposure bias   :
Flash           :
Flash bias      :
Focal length    :
Subject distance:
ISO speed       :
Exposure mode   :
Metering mode   :
Macro mode      :
Image quality   :
White balance   :
Copyright       :
Exif comment    :


****Audio*****

foremost -i audio.wav: No hidden data in footer/header

---------Stegseek---------

stegseek --seed audio.wav

error: Could not find a valid seed.

--------------Exiftool message2.wav:--------------
ExifTool Version Number         : 12.40
File Name                       : message2.wav
Directory                       : .
File Size                       : 11 MiB
File Modification Date/Time     : 2023:10:04 05:48:26+02:00
File Access Date/Time           : 2023:10:04 05:49:04+02:00
File Inode Change Date/Time     : 2023:10:04 05:48:45+02:00
File Permissions                : -rw-rw-r--
File Type                       : WAV
File Type Extension             : wav
MIME Type                       : audio/x-wav
Encoding                        : Microsoft PCM
Num Channels                    : 2
Sample Rate                     : 48000
Avg Bytes Per Sec               : 192000
Bits Per Sample                 : 16
Artist                          : CTF
ID3 Size                        : 20
Duration                        : 0:01:02

----------exiv2-------------------

File name       : message2.wav
File size       : 11888756 Bytes
MIME type       : video/riff
Image size      : 0 x 0

--------------FFMPEG-----------------

ffmpeg -v info - i message2.wav -f null

ffmpeg version 4.4.2-0ubuntu0.22.04.1 Copyright (c) 2000-2021 the FFmpeg developers
  built with gcc 11 (Ubuntu 11.2.0-19ubuntu1)
  configuration: --prefix=/usr --extra-version=0ubuntu0.22.04.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libdav1d --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librabbitmq --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libsrt --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzimg --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-pocketsphinx --enable-librsvg --enable-libmfx --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared
  libavutil      56. 70.100 / 56. 70.100
  libavcodec     58.134.100 / 58.134.100
  libavformat    58. 76.100 / 58. 76.100
  libavdevice    58. 13.100 / 58. 13.100
  libavfilter     7.110.100 /  7.110.100
  libswscale      5.  9.100 /  5.  9.100
  libswresample   3.  9.100 /  3.  9.100
  libpostproc    55.  9.100 / 55.  9.100
Trailing option(s) found in the command: may be ignored.
[wav @ 0x55ed434685c0] Discarding ID3 tags because more suitable tags were found.
Guessed Channel Layout for Input Stream #0.0 : stereo
Input #0, wav, from 'message2.wav':
  Metadata:
    artist          : CTF
  Duration: 00:01:01.92, bitrate: 1536 kb/s
  Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 48000 Hz, stereo, s16, 1536 kb/s
