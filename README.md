```bash
###################################
#                                 #
#          Knife Linux            #
#    A Kali live-build recipe     #
#                                 #
#       Authored by kaneda        #
#                                 #
#    Shoutouts to:                #
#      #masshackers, ##hackers,   #
#      #kali-linux on Freenode    #
#                                 #
###################################
```

Knife
=====

Knife is essentially a Kali live-build recipe that includes a bunch of admin tools found in Debian as well as some tools and frameworks that are little-known outside of the professional security community.

[![Documentation Status](https://readthedocs.org/projects/knife-linux/badge/?version=latest)](https://readthedocs.org/projects/knife-linux/?badge=latest)


Installing
==========

##Pre-build checklist:

1) Get Kali. This build process uses only Kali repos, and therefore building from a vanilla Debian system (or other Debian derivative) is *not recommended*

2) Add the Kali key to your apt-keys
```bash
$ sudo wget -q -O - https://www.kali.org/archive-key.asc | gpg --import
$ sudo wget -q -O - https://www.kali.org/archive-key.asc | sudo apt-key adv
$ sudo apt-key adv --keyserver pgp.mit.edu --recv-keys ED444FF07D8D0BF6
$ sudo apt-get update
```

3) Update your apt-cache and your system
```bash
$ apt-get update && apt-get upgrade -y
```

4) Now get your dependencies:
```bash
$ apt-get install git live-build cdebootstrap kali-archive-keyring
```

5) Get the Knife live-build recipe:
```bash
$ git clone https://github.com/kaneda/knife.git
```
- Check out Kali's original recipe (if you're interested):
```bash
$ git clone git://git.kali.org/live-build-config.git
```

##To build:

### Before you begin

Check out the notes below this section on installing apt-cacher-ng. If you wish to use apt-cacher-ng a small amount of additional setup is required. Warning, apt-cacher-ng has issues with slower connections, including a lot of missing/corrupted headers, as well as timeouts.

I've used the current stable kernel (3.14) from Kali explicitly due to issues with aufs no longer being supported.

The finished build, which includes an ISO, will take up more than 25GB of space.

### Build steps

From within the live-build-config directory

1)
```bash
$ lb clean --purge
```
2) This only needs to be done once
```bash
$ dpkg --add-architecture amd64
```
3) This should be done regularly, but is not necessary before each biuld
```bash
$ apt-get update
```
4) This must be done in the term in which you're building before builds
```bash
$ export http_proxy=http://localhost:3142/
```
  - Note that this only applies when using apt-cacher-ng (see note 2 below)

5)
```bash
$ lb config
```
- Note that I've modified the auto/config lb config so that no additional settings are required. If you set http_proxy (as above) auto/config will pick up these settings automatically now.

6)
```bash
$ lb build
```
7) You'll find your completed build in the live-build-config folder

##Notes 

1) Steps two and three are unecessary after the first run (though you may want to update package sources daily).

2) You can use apt-cacher-ng to cache your packages (so that you won't need to download them from the repos upon each build). This is useful if you plan to do a lot of builds in a short time. This is *highly recommended*.
- Check out http://www.tecmint.com/apt-cache-server-in-ubuntu/ for how to configure apt-cacher-ng
- Check out http://docs.kali.org/downloading/live-build-a-custom-kali-iso for instructions related to apt-cacher-ng and live-build
- You will need to add a line in the config for Kali:
```bash
Remap-debrep: file:kali /kali ; file:backends_kali # Kali Archives
Remap-debrep: file:kali_security* /kali-security ; file:backends_kali_security # Kali Archives
```
- You must then create the backends_kali file in the /etc/apt-cacher-ng directory:
```bash
http://http.kali.org/kali
```
- Likewise a backends_kali_security file:
```bash
http://security.kali.org/kali-security
```
- Next add a proxy config to your apt.conf.d (e.g., /etc/apt/apt.conf.d/01proxyconf):
```
Acquire::http { Proxy "http://127.0.0.1:3142"; };
```
  - Note that this is just like doing so for something like Polipo
- Before you configure (in step 4 above) ensure that apt-cacher-ng is started and export your http proxy variable (see step 3 and the last part of 4 above for use):
```bash
export http_proxy=http://localhost:3142/
```

FAQ
===

Q: For whom did you make this?
A: For security professionals, in order to give them immediate and easy access to new tools that I've discovered, as well as the administrative power of tools already found in Debian repos


Q: Couldn't they just do it themselves?
A: Of course, if they they wanted to spend the many hours of discovery to find the tools, many of which come from being a Linux administrator


Q: How long did this take to build?
A: The initial setup took between 15 and 20 hours


Q: Isn't this essentially just Kali?
A: Yes, and that's the point: this isn't so much its own distribution as an expansion to Kali, to which this distro pays homage. It includes additions to iceweasel, ruby tools, NMAP, and many interesting administrative tools, that are not well-known (see wiki or the list below).


Q: Weren't you the lead developer on AttackVector?
A: Yes, but due to differences of opinion (in which the organizer repeatedly damaged the project), and because I do not agree with providing a hand-cannon to nubblets (you can feel free to install and configure TOR yourself), I have left the project to pursue my own design goals (as aforementioned)


# Tools

##From Debian

###For Hashkill
- libssl-dev 
- libjson0-dev
- amd-opencl-dev
- nvidia-opencl-dev

###For everything else
- adduser
- binutils
- bsdutils
- chkconfig
- coreutils
- curl
- diffutils
- dnsutils
- dsniff
- findutils
- florence
- fuse-utils
- gnupg
- gnupg-agent
- gnupg-curl
- gnutls-bin
- gzip
- haveged
- ipheth-utils
- iproute
- iptstate
- iputils-ping
- iputils-tracepath
- john
- john-data
- keepassx
- laptop-mode-tools
- libsqlite3-dev
- libsqlite3-ruby1.9.1
- liferea
- liferea-data
- lockfile-progs
- lua5.1
- lzma
- moreutils
- mtools
- ncurses-base
- ncurses-bin
- net-tools
- netcat-traditional
- openssl
- poppler-utils
- pwgen
- rfkill
- ruby1.9.1
- ruby1.9.1-dev
- rubygems
- secure-delete
- sqlite3
- ssss
- unar
- unzip
- vim-nox
- vim-runtime
- wget
- whois

##From gems
- ronin (https://github.com/ronin-ruby/)
- ronin-asm
- ronin-dorks
- ronin-exploits
- ronin-gen
- ronin-grid
- ronin-php
- ronin-scanners
- ronin-sql
- ronin-support
- ronin-web

##From the web
- hashkill (https://github.com/gat3way/hashkill/)
- quicksnap (https://www.soldierx.com/sxlabs/quicksnap-Customized-Automatic-Scanner-Nmap)

# License / Open Source Policy

Knife, as a derivative of Kali (and therefore Debian) complies with the Debian Free Software Guidelines. See Kali's open source policy (http://docs.kali.org/kali-policy/kali-linux-open-source-policy) about how this complies with Debian's policies, but also the non-free section that designates allowed redistribution of certain software through default or specific license agreements.

Likewise Knife has obtained default or specific license agreements to redistribute some of the additional software above from the creators.

In addition to the GPL licensing I also ask that, as a courtesy, you leave all headers in place giving credit to the creators of scripts, software, etc. If you choose to modify the software/script/etc. you may make an amendment to the header to denote contribution, but under no circumstances should you remove existing header information.

