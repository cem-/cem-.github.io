<article markdown="1">

<header markdown="1">
 
# Windows 8 and Bluetooth

<time class="pubdate" datetime="2013-01-02">2013-01-02</time>

</header>
The problem: brand new Windows 8 install, Bluetooth not working, not present in device manager. All drivers updated, BIOS updated, manufacturer software installed...

The hardware: Lenovo ThinkPad T500, Broadcom Bluetooth

When I upgraded my Windows 7 install to Windows 8, I choose the option that did not keep any files or settings (in order to have a clean install). My Bluetooth when I began the process was turned off, and as the hardware was shut off in the settings, apparently Windows 8 was unable to even find the existence of the Bluetooth modem. It was not present in device manager, thus I was unable to install drivers for it. Therefore, I postulated, if I could somehow get the hardware turned on, Windows 8 would be able to see it.

To turn on the Bluetooth modem, I created an Ubuntu USB drive, booted to that, verified that the Bluetooth was turned on, then rebooted to the Windows install. As I expected, the Bluetooth modem stayed on, and I am now able to turn the Bluetooth on and off via the Windows settings UI.

My advice, just in case, make sure you turn on Bluetooth before you upgrade...

</article>
