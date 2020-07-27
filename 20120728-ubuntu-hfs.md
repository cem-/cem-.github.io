<article markdown="1">

<header markdown="1">
 
# Recovering Data from an iMac to HFS+ via an Ubuntu Live Disk

<time class="pubdate" datetime="2012-07-28">2012-07-28</time>

</header>

Recently I volunteered to fix a friends iMac, the symptoms were Safari running extremely slowly, causing system freezes. Oddly enough, Firefox worked happily along with no issues. I thought, “maybe the software is out of date, perhaps a new version of Safari would fix this, or maybe some software has caused a conflict somehow.” In attempting to update the OS, the disk failed. “Well,” I thought, “that explains the system freezes”. The following are the steps I took to recover the data and bring back the OS.

First, I contacted my friend (let’s call him Aaron) to garner any assistance he could provide, he works with Apples’ more frequently than I, so I figured that would be a great starting place. After some help from him for various ways to update and run live OSX utilities from install disks I set out to recover the data. Thank you friend “Aaron”.

First I tried SpinRite, the keyboard did not work! It turns out that it does not work on Apples due to the EFI rather than BIOS being used on on Macs.

"The INT’s from BIOS are used also to access the disks, so all the methods need to be translated to EFI"

-Steve Gibson

Excerpt from Security Now #293:

> I wish I could easily get the hard drive out of my iMac, it's a real pain, because my son's hard drive crashed.  And I'm sure I could put it in a PC, SpinRite it, and it would all be fine.  But the iMac, the big negative, you have to actually take suction cups and remove the glass.  It's very - it's ridiculous.  Colleen did it, she's got more nerve than I did, some time ago when the hard drive on my iMac here died.  And I remember watching her do it.  And I thought, oh, geez.  Oh, geez.  I ain't doing that.  No user-serviceable parts inside there.

Thus I knew the only way to SpinRite it would be removing the glass front with suction cups... I’d rather not.

I opted for an Ubuntu install disk instead. Booting into Ubuntu worked great, the problem was the 2TB Seagate GoFlex I had to transfer the files to was unreadable due to permissions that Ubuntu respects. After some Googleing I found instructions for allowing read/write access to the HFS+ file system Apple uses. <a target="_blank" href="http://mac.linux.be/phpBB3/viewtopic.php?f=14&amp;t=95">(here)</a> For Ubuntu, the instructions linked to are pretty much the same. However, when I logged back in as the Ubuntu live user, I could not make a new folder to back up the bad drive to on the Seagate. It turns out, Ubuntu cannot write to HFS+ unless it is non- journaled. To disable journaling, one must boot to the OSX install disk, start the Disk Utility, then hold the command key and click File->Disable Journaling. <a target="_blank" href="http://superuser.com/questions/84446/how-to-mount-a-hfs-partition-in-ubuntu-as-read-write">(source)</a>

  <dl>
  <dt>To conclude, when you need to get data from an iMac to a journaled HFS+ external drive, follow these steps:</dt>
  <dd>
  <dl><dt>Boot to Mac OSX install disk</dt>
  <dd><a target="_blank" href="http://guides.macrumors.com/Mac_doesn't_boot">http://guides.macrumors.com/Mac_doesn't_boot</a></dd>
  <dd>Start with step 5</dd>
  </dl>
  
  <dl>
  <dt>Disable journaling</dt>
  <dd><a target="_blank" href="http://superuser.com/questions/84446/how-to-mount-a-hfs-partition-in-ubuntu-as-read-write">http://superuser.com/questions/84446/how-to-mount-a-hfs-partition-in-ubuntu-as-read-write</a></dd>
  </dl>
  
  <dl>
  <dt>Boot into a live Ubuntu install disk</dt>
  <dd><a target="_blank" href="http://www.ubuntu.com/download/help/create-a-usb-stick-on-mac-osx">http://www.ubuntu.com/download/help/create-a-usb-stick-on-mac-osx</a></dd>
  </dl>
  
  <dl>
  <dt>Change the default Ubuntu use’s permissions to allow access to both the OSX hard drive and the external drive</dt>
  <dd><a target="_blank" href="http://mac.linux.be/phpBB3/viewtopic.php?f=14&amp;t=95">http://mac.linux.be/phpBB3/viewtopic.php?f=14&amp;t=95</a></dd>
  </dl>
  
  <dl>
  <dt>Open terminal and rsync the files</dt>
  <dd><code>rsync –av –ignore-errors /media/OSX_HardDrive /media/ExternalDrive</code></dd>
  </dl>
  
  </dd>
  </dl>
  
</article>
