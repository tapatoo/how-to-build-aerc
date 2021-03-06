# How to Build Aerc Mail Client

These instructions are for debian based distributions and will work with Raspberry Pi if a recent version of golang is installed.

## Install dependencies
```shell
sudo apt install w3m dante-client libnotmuch-dev scdoc poppler-utils catimg checkinstall
```

- `w3m` - render html in terminal
- `dante-client` - installs socksify to assist with rendering html locally
- `libnotmuch-dev` - required to compile `notmuch` into the client
- `scdoc` - renders document templates during build time
- `poppler-utils` - provides `pdftotext` to allow converting pdfs to view in client
- `catimg` - allows "viewing" images in terminal window
- `checkinstall` - script to assist with building a package

## Get source code
```shell
git clone https://git.sr.ht/~sircmpwn/aerc
cd aerc
```

## Build

```shell
make GOFLAGS=-tags=notmuch PREFIX=/usr/local
```

In some cases with older versions of `scdoc`compilation might end in error when trying to process `aerc-templates.7`. Don't worry all the relevant stuff compiles and the templates can be defined in your own time:

```shell
scdoc < doc/aerc-templates.7.scd > aerc-templates.7
Error at 32:3: Cannot deindent in literal block
make: *** [Makefile:48: aerc-templates.7] Error 1
```

## Create a package

```shell
> sudo checkinstall

checkinstall 1.6.2, Copyright 2009 Felipe Eduardo Sanchez Diaz Duran
           This software is released under the GNU GPL.


The package documentation directory ./doc-pak does not exist.
Should I create a default set of package docs?  [y]: y

Preparing package documentation...OK

Please write a description for the package.
End your description with an empty line or EOF.
>> Email Client for your Terminal
>>

*****************************************
**** Debian package creation selected ***
*****************************************

This package will be built according to these values:

0 -  Maintainer: [ root@pi ]
1 -  Summary: [ Email Client for your Terminal ]
2 -  Name:    [ aerc ]
3 -  Version: [ 20200419 ]
4 -  Release: [ 1 ]
5 -  License: [ GPL ]
6 -  Group:   [ checkinstall ]
7 -  Architecture: [ armhf ]
8 -  Source location: [ aerc ]
9 -  Alternate source location: [  ]
10 - Requires: [  ]
11 - Provides: [ aerc ]
12 - Conflicts: [  ]
13 - Replaces: [  ]

Enter a number to change any of them or press ENTER to continue: 0

Enter the maintainer\'s name and e-mail address:                                                                                                               
>> user@system

This package will be built according to these values:

0 -  Maintainer: [ user@system ]
1 -  Summary: [ Email Client for your Terminal ]
2 -  Name:    [ aerc ]
3 -  Version: [ 20200419 ]
4 -  Release: [ 1 ]
5 -  License: [ GPL ]
6 -  Group:   [ checkinstall ]
7 -  Architecture: [ armhf ]
8 -  Source location: [ aerc ]
9 -  Alternate source location: [  ]
10 - Requires: [  ]
11 - Provides: [ aerc ]
12 - Conflicts: [  ]
13 - Replaces: [  ]

Enter a number to change any of them or press ENTER to continue: 6
Enter the new software group:
>> email

This package will be built according to these values:

0 -  Maintainer: [ user@system ]
1 -  Summary: [ Email Client for your Terminal ]
2 -  Name:    [ aerc ]
3 -  Version: [ 20200419 ]
4 -  Release: [ 1 ]
5 -  License: [ GPL ]
6 -  Group:   [ email ]
7 -  Architecture: [ armhf ]
8 -  Source location: [ aerc ]
9 -  Alternate source location: [  ]
10 - Requires: [  ]
11 - Provides: [ aerc ]
12 - Conflicts: [  ]
13 - Replaces: [  ]

Enter a number to change any of them or press ENTER to continue:

Installing with make install...

========================= Installation results ===========================
mkdir -m755 -p /usr/local/bin /usr/local/share/man/man1 /usr/local/share/man/man5 /usr/local/share/man/man7 \
        /usr/local/share/aerc /usr/local/share/aerc/filters /usr/local/share/aerc/templates
install -m755 aerc /usr/local/bin/aerc
install -m644 aerc.1 /usr/local/share/man/man1/aerc.1
install -m644 aerc-search.1 /usr/local/share/man/man1/aerc-search.1
install -m644 aerc-config.5 /usr/local/share/man/man5/aerc-config.5
install -m644 aerc-imap.5 /usr/local/share/man/man5/aerc-imap.5
install -m644 aerc-maildir.5 /usr/local/share/man/man5/aerc-maildir.5
install -m644 aerc-sendmail.5 /usr/local/share/man/man5/aerc-sendmail.5
install -m644 aerc-notmuch.5 /usr/local/share/man/man5/aerc-notmuch.5
install -m644 aerc-smtp.5 /usr/local/share/man/man5/aerc-smtp.5
install -m644 aerc-tutorial.7 /usr/local/share/man/man7/aerc-tutorial.7
install -m644 aerc-templates.7 /usr/local/share/man/man7/aerc-templates.7
install -m644 config/accounts.conf /usr/local/share/aerc/accounts.conf
install -m644 aerc.conf /usr/local/share/aerc/aerc.conf
install -m644 config/binds.conf /usr/local/share/aerc/binds.conf
install -m755 filters/hldiff /usr/local/share/aerc/filters/hldiff
install -m755 filters/html /usr/local/share/aerc/filters/html
install -m755 filters/plaintext /usr/local/share/aerc/filters/plaintext
install -m644 templates/quoted_reply /usr/local/share/aerc/templates/quoted_reply
install -m644 templates/forward_as_body /usr/local/share/aerc/templates/forward_as_body

======================== Installation successful ==========================

Copying documentation directory...
./
./LICENSE
./README.md
./doc/
./doc/aerc.1.scd
./doc/aerc-maildir.5.scd
./doc/aerc-sendmail.5.scd
./doc/aerc-imap.5.scd
./doc/aerc-templates.7.scd
./doc/aerc-search.1.scd
./doc/aerc-config.5.scd
./doc/aerc-notmuch.5.scd
./doc/aerc-smtp.5.scd
./doc/aerc-tutorial.7.scd

Copying files to the temporary directory...OK

Stripping ELF binaries and libraries...OK

Compressing man pages...OK

Building file list...OK

Building Debian package...OK

Installing Debian package...OK

Erasing temporary files...OK

Deleting temp dir...OK


**********************************************************************

 Done. The new package has been installed and saved to

 /home/dietpi/Downloads/aerc/aerc_20200419-1_armhf.deb

 You can remove it from your system anytime using:

      dpkg -r aerc

**********************************************************************
```

# Run `aerc` the first time and complete initial configuration

After the initial configuration you will have a few configuration files in `~/.config/aerc`:

**accounts.conf** - this is where you configure your email accounts:

Config format:
```
[personal]
source        = imaps://someusers%40gmail.com:somepassword@imap.gmail.com:993
outgoing      = smtp+plain://someusers%40gmail.com:somepassword@smtp.gmail.com:587
default       = INBOX
smtp-starttls = yes
from          = Full Name <someuser@gmail.com>
copy-to       = Sent
```

For Gmail accounts you will need to generate an application password as described in [Google Documentation](https://support.google.com/accounts/answer/185833?hl=en).

**aerc.conf** - has got a few interesting configuration options. This file allows defining filters that will help with rendering `html` or `pdf` in aerc. I have the following filters defined:

```shell
[filters]

# This filter will render html
text/html=/usr/local/share/aerc/filters/html
# This will converst a pdf file to text
application/pdf=pdftotext - - | less
# This will display images in terminal
image/*=catimg -w $(tput cols) -
# Alternatively you could use \display\
image/*=display # Won't work if X isn't installed


# Set your favourite editor to be able to compose messages

[compose]

#
# Specifies the command to run the editor with. It will be shown in an embedded
# terminal, though it may also launch a graphical window if the environment
# supports it. Defaults to $EDITOR, or vi.
editor=vim
```