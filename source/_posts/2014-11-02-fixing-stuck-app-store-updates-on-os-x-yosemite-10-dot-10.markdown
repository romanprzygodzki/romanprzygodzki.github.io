---
layout: post
title: "fixing stuck app store updates on OS X Yosemite 10.10"
date: 2014-11-02 12:33:28 -0500
comments: true
categories: mac OS_X
---

After updating to Mac OS X Yosemite, I ran into an issue where the Mac App Store kept thinking I had an update to install for Garageband. After searching the internets, I noticed others having similar problems, but I couldn't find a solution that worked. After some tinkering, I was able to find a fix. 

<!-- more -->

Unlike Vinny, six times was not a charm...

After the sixth time I attempted to update Garageband to version 10.0.3, I went to the <code>Applications</code> folder and noticed that Garageband remained at version 10.0.2. So it seemed like the update was downloaded but failed to install. Here is my solution:

(1) Save any unsaved work.<br>
(2) Open the Mac App Store.<br>
(3) Go to <code>Store</code> then <code>Sign Out</code>.<br>
(4) Quit the Mac App Store.<br>
(5) You didn't skip step (1), did you? If you did, save any unsaved work before proceeding. Losing unsaved work is not fun.<br>
(6) Log out of your user *but be sure to uncheck the* <code>Reopen windows when logging back in</code> *checkbox.* This is why it is important to do step 1, *otherwise you'll lose any unsaved work!*<br>
(7) Log back into your user.<br>
(8) Open the Mac App Store and run the software updates.<br>
(9) Your updates will hopefully install successfully. Exclaim *huzzah* if they do!<br>
(10) Because we unchecked <code>Reopen windows when logging back in</code> in step 6, it will remain unchecked unless you specify otherwise. If you use this feature, log out and check on <code>Reopen windows when logging back in</code> so you don't lose unsaved work the next time you log off.