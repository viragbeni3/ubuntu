# Unattended Ubuntu ISO Maker

This simple script will create an unattended Ubuntu ISO from start to finish. It will ask you a few questions once, and embed your answers into a remastered ISO file for you to use over and over again.

This script creates a 100% original Ubuntu installation; no additional software is added (aside from the VMWare OSP Tools, which are optional), not even an ```apt-get update``` is performed. You have all the freedom in the world to customize your Ubuntu installation whichever way you see fit. This script just takes the pain out of re-installing Ubuntu over and over again.

Consider using tools like chef or puppet to perform any additional software installations/configurations. 

Original created by: **Rinck Sonnenberg (Netson)**

## Compatibility

The script supports the following Ubuntu editions out of the box:

* Ubuntu 16.04 Server LTS amd64 - Xenial Xerus

Script automatically chooses the latest current image by parsing http://releases.ubuntu.com page.

This script has been tested on and with these three versions as well, but I see no reason why it shouldn't work with other Ubuntu editions. Other editions would require minor changes to the script though.

## Usage

* From your command line, run the following commands:

```
$ wget https://github.com/englert/ubuntu-iso/master/ubuntu-iso.sh
$ chmod +x create-unattended-iso.sh
$ sudo ./create-unattended-iso.sh

 +---------------------------------------------------+
 |            UNATTENDED UBUNTU ISO MAKER            |
 +---------------------------------------------------+

 which ubuntu edition would you like to remaster:

* Sit back and relax, while the script does the rest! :)

## What it does

This script does a bunch of stuff, here's the quick walk-through:

* It asks you for your preferences regarding the unattended ISO
* Downloads the appropriate Ubuntu original ISO straight from the Ubuntu servers; if a file with the exact name exists, it will use that instead (so it won't download it more than once if you are creating several unattended ISO's with different defaults)
* Downloads the netson preseed file; this file contains all the magic answers to auto-install ubuntu. It uses the following defaults for you (only showing most important, for details, simply check the seed file in this repository):
 * Language/locale: en_US
 * Keyboard layout: HU_hu
 * Root login disabled (so make sure you write down your default usernames' password!)
 * Partitioning: LVM, full disk, single partition
* Install the mkpasswd program (part of the whois package) to generate a hashed version of your password
* Install the genisoimage program to generate the new ISO file
* Mount the downloaded ISO image to a temporary folder
* Copy the contents of the original ISO to a working directory
* Set the default installer language
* Add/update the preseed file
* Add the autoinstall option to the installation menu
* Generate the new ISO file
* Cleanup
* Show a summary of what happended:

```  
 installing required packages
 remastering your iso file
 creating the remastered iso
 -----
 finished remastering your ubuntu iso file
 the new file is located at: /tmp/ubuntu-16.04.4​
36
  
37
  [3] Ubuntu 16.04.1 Server LTS amd64 - Xenial Xerus
38
​
39
 
40
​
41
* Enter your desired timezone; the default is *Europe/Budapest*:
42
​
43
```
44
 please enter your preferred timezone: Europe/Budapest
45
```
46
​
47
username default is *ubuntu*:
48
​
49
```
50
 please enter your preferred username: ubuntu
51
```
52
​
53
password:123456
54
```
55
​
56
-server-amd64-unattended.iso
 your username is: ubuntu
 your password is: 
 your hostname is: ubuntu
 your timezone is: Europe/Budapest
```

### Once Ubuntu is installed ...

Just fire off the start.sh script in your users' home directory to complete the installation. This will ask you if you would like to add the puppetlabs repositories for puppet and its dependencies and if you would also like to setup the puppet agent

```$ sudo ~/start.sh``` 

### That's it, enjoy! :)

## Troubleshooting

If you run into any issues, please create an issue; I am by no means a shell/bash expert (far from it), and it took me a while to compile this script into something that's easy to use and just works, but I'm happy to help where I can! :)

## License
MIT
