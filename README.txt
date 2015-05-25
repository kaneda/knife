###################################
#                                 #
#          Knife Linux            #
#    A Kali live-build recipe     #
#                                 #
#       Authored by kaneda        #
#                                 #
#    Shoutouts to:                #
#      Hardcoded, Masshackers     #
#                                 #
###################################

Knife
=====

Knife is essentially a Kali live-build recipe that includes a bunch of admin tools found in Debian as well as some tools and frameworks that are little-known outside of the professional security community.

[![Documentation Status](https://readthedocs.org/projects/knife-linux/badge/?version=latest)](https://readthedocs.org/projects/knife-linux/?badge=latest)

Installing
==========

##Pre-build checklist:

1) apt-get install git live-build cdebootstrap kali-archive-keyring
2) git clone https://user@bitbucket.org/kanedasan/knife-linux.git
	a) Check out Kali's: git clone git://git.kali.org/live-build-config.git


##To build:

1) lb clean --purge
2) dpkg --add-architecture amd64
3) apt-get update
4) lb config --bootappend-live "hostname=knife" --architecture amd64 --mirror-binary http://http.kali.org/kali --mirror-binary-security http://security.kali.org/kali-security --apt-options "--force-yes --yes"
5) lb build

##Notes 

1) Steps two and three are unecessary after the first run.
2) You can use apt-cacher-ng to cache your packages (so that you won't need to download them from the repos upon each build). This is useful if you plan to do a lot of builds in a short time.



FAQ
===

Q For whom did you make this?
A For security professionals, in order to give them immediate and easy access to new tools that I've discovered, as well as the administrative power of tools already found in Debian repos

Q Couldn't they just do it themselves?
A Of course, if they they wanted to spend the many hours of discovery to find the tools, many of which come from being a Linux administrator

Q How long did this take to build?
A The initial setup took between 15 and 20 hours

Q Isn't this essentially just Kali?
A Yes, and that's the point: this isn't so much its own distribution as an expansion to Kali, to which this distro pays homage. It includes additions to iceweasel, ruby tools, NMAP, and many interesting administrative tools, that are not well-known (see wiki or the list below).

Q Weren't you the lead developer on AttackVector?
A Yes, but due to differences of opinion (in which the organizer repeatedly damaged the project), and because I do not agree with providing a hand-cannon to nubblets (you can feel free to install and configure TOR yourself), I have left the project to pursue my own design goals (as aforementioned)



Tools
=====

##From Debian

###For Hashkill
libssl-dev 
libjson0-dev
amd-opencl-dev
nvidia-opencl-dev

###For everything else
adduser
binutils
bsdutils
chkconfig
coreutils
curl
diffutils
dnsutils
dsniff
findutils
florence
fuse-utils
gnupg
gnupg-agent
gnupg-curl
gnutls-bin
gzip
haveged
ipheth-utils
iproute
iptstate
iputils-ping
iputils-tracepath
john
john-data
keepassx
laptop-mode-tools
libsqlite3-dev
libsqlite3-ruby1.9.1
liferea
liferea-data
lockfile-progs
lua5.1
lzma
moreutils
mtools
ncurses-base
ncurses-bin
net-tools
netcat-traditional
openssl
poppler-utils
pwgen
rfkill
ruby1.9.1
ruby1.9.1-dev
rubygems
seahorse
seahorse-nautilus
secure-delete
sqlite3
ssss
unar
unzip
vim-nox
vim-runtime
wget
whois

##From gems
ronin (https://github.com/ronin-ruby/)
ronin-asm
ronin-dorks
ronin-exploits
ronin-gen
ronin-grid
ronin-php
ronin-scanners
ronin-sql
ronin-support
ronin-web

##From the web
hashkill (https://github.com/gat3way/hashkill/)
fakeap (http://www.blackalchemy.to/project/fakeap/)
quicksnap (https://www.soldierx.com/sxlabs/quicksnap-Customized-Automatic-Scanner-Nmap)
