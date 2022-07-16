# extract_payload
 Extract the installation payload from a Big Sur style macOS Installer

A simple tool to extract the contents of a macOS Big Sur installer
to a desired destination. Note that this does not create a bootable
installation of Big Sur as it simply dumps the contents of the
instal to a folder.

When initially reverse engineering the macOS Big Sur installer when
Developer Preview 1 was released, I was stumped by the payload.XYZ
file format. I reviewed existing work by Johnathan Levin
(http://newosxbook.com/articles/OTA.html) and my previous code for
PBZX streams used when reverse engineering the Apple T2 Chip 
(https://github.com/toru173/parse_pbzx), but I was unable to make
headway.

I've since had reason to revisit this for a new project. An
interesting point on the iPhone Wiki drew my eye:

The payload.000-999 files use the AppleArchive compression.
They can be extracted using the built-in macOS yaa command line
tool or by adding the .aar extension and opening the file with the 
built-in macOS Archive Utility or Keka.

(from https://www.theiphonewiki.com/wiki/OTA_Updates)

I was indeed able to extract the payload files by appending .aar
to them. This, we are able to extract the payload files without
ever dealing with the pbzx streams directly! /usr/bin/yaa is a 
symlink to /usr/bin/aa so the script uses the later directly.
