<article markdown="1">

<header markdown="1">
 
# Google Voice and The Linux Command Line

<time class="pubdate" datetime="2010-08-13">2010-08-13</time>

</header>

So, my email being sent using the (Ubuntu) Linux was being blocked by the ISP, Gmail, and other mail servers (Exchange) therefore, I decided to find an alternative way to get alerts from my server. Enter Google Voice and their SMS feature. I found that I can send text messages to myself, thus allowing for instantaneous alerting of events. (the following assumes that you are running ubuntu)

first run these commands:

```
------------------------------------------------------------------------
sudo apt-get install python python-simplejson python-setuptools
wget http://pygooglevoice.googlecode.com/files/pygooglevoice-0.5.tar.gz
tar -zxvf pygooglevoice-0.5.tar.gz
cd pygooglevoice-0.5
sudo apt-get install python python-setuptools
cd ~/
touch bin/smsme
chmod +x bin/smsme
vim bin/smsme
------------------------------------------------------------------------
```

Then, open vim and do a ':set paste'
paste in the code below
after pasting press esc and do a ':set paste!'

```
------------------------------------------------------------------------
#!/usr/bin/python
import sys
from googlevoice import Voice
from googlevoice.util import input
// replace with your g-voice phone number
phone_numb=5555555555
voice = Voice()
voice.login()
text = ' '.join(sys.argv[1:])
voice.send_sms(phone_numb, text)
------------------------------------------------------------------------
```
make any changes to the code, then do a :wq to exit

Also, you should edit the file in your home directory '.gvoice' and add your username and password (make sure you chmod 600 on that file though..)

Now, you can type in at the command line:

`smsme <message>`

For Example:
```smsme there's a fly in your soup... i mean server. fix it!```

You will recieve a message on your phone "there's a fly in your soup... i mean server. fix it!"

Stay tuned for useful uses for this smsme script.

</article>
