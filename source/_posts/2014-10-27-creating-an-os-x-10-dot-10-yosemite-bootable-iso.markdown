---
layout: post
title: "creating a Mac OS X 10.10 Yosemite ISO"
date: 2014-10-27 23:21:00 -0400
comments: true
categories: mac OS_X terminal
---

Here are instructions on how to create an ISO of OS X Yosemite 10.10. This might be helpful in the event that a future OS release (e.g. 10.10.1) breaks *that one program* (or four...) that must work and you need to roll back to a prior version of the OS. Hopefully you'll never need to rely on a backup ISO but if you do, you are prepared!

Slowly input these commands into Terminal. These worked for me when I used them, but please note that if this erases something on your machine, magically makes you coffee or conjures gnomes, I take no responsibility.

``` bash How to make a Mac OS X 10.10 Yosemite ISO
# Mount the Yosemite installer image.
hdiutil attach /Applications/Install\ OS\ X\ Yosemite.app/Contents/SharedSupport/InstallESD.dmg -noverify -nobrowse -mountpoint /Volumes/install_app

# Convert the Yosemite image to a sparseimage. This will hold the necessary components.
hdiutil convert /Volumes/install_app/BaseSystem.dmg -format UDSP -o /tmp/Yosemite

# Expand the size of the sparseimage so that it can hold the remaining files.
hdiutil resize -size 8g /tmp/Yosemite.sparseimage

# Mount the sparseimage.
hdiutil attach /tmp/Yosemite.sparseimage -noverify -nobrowse -mountpoint /Volumes/install_build

# Move the Yosemite files to your sparseimage.
# This may take a little depending on the speed of your drive. Enjoy a coffee!
rm /Volumes/install_build/System/Installation/Packages
cp -rp /Volumes/install_app/Packages /Volumes/install_build/System/Installation/
cp -rp /Volumes/install_app/BaseSystem.chunklist /Volumes/install_build
cp -rp /Volumes/install_app/BaseSystem.dmg /Volumes/install_build

# Unmount the Yosemite installer image and sparseimage.
hdiutil detach /Volumes/install_app
hdiutil detach /Volumes/install_build

# Remove free space from the sparseimage so that it won't take up 8GB.
hdiutil resize -size `hdiutil resize -limits /tmp/Yosemite.sparseimage | tail -n 1 | awk '{ print $1 }'`b /tmp/Yosemite.sparseimage

# Convert to a cdr.
hdiutil convert /tmp/Yosemite.sparseimage -format UDTO -o /tmp/Yosemite

# Delete the sparseimage, since you created a cdr in the prior step.
rm /tmp/Yosemite.sparseimage

# Move the cdr to the desktop and rename it from a cdr to an ISO.
mv /tmp/Yosemite.cdr ~/Desktop/Yosemite.iso

# Throw your hands in the air and exclaim "huzzah!!" You're done.
```