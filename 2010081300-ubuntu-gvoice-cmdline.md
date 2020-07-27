<article markdown="1">

<header markdown="1">
 
# cron Monitoring for IP Address Changes and SMSing via Google Voice

<time class="pubdate" datetime="2010-08-13">2010-08-13</time>

</header>

In the previous post, i mentioned that I would have some uses for the smsme script that I wrote. Here's a script that checks your external IP address against what you have registered in the DNS system, and alerts you when the address changes.

Also, I've included instructions for creating a user cron job to check every hour on the hour.

```
------------------------------------------------------------------------
#!/bin/bash
DNS=`nslookup cem.me 8.8.8.8 | grep 'Address: ' | grep -Eo '[0-9\.]+'`
EXTIP=`wget -q -O - http://checkip.dyndns.org | grep -Eo '[0-9\.]+'`
if [ $DNS != $EXTIP ] ;
&nbsp;&nbsp;then
&nbsp;&nbsp; &nbsp;`/home/username/bin/smsme IP CHANGED: $EXTIP`
fi
------------------------------------------------------------------------
```

The DNS command goes to Google’s DNS, pipes the output to search for 'Address:' followed by a space, and then pulls out the IP address.

The EXTIP goes to http://checkip.dyndns.org and parses out your IP

To create the cron job, create a new file (crontab.<username>.file) and enter in the text below:

`0 * * * * /home/<username>/bin/checkip.sh`

This line says (in the 0 `* * * *`) part to run on the hour `(00)`, every hour `(*)`, every day `(*)`, every month`(*)`, every day of the week`(*)` and will run our script that we wrote above (/home/<username>/bin/checkip.sh) make sure you replace the <username> part with your username

```
#this allows your user to run cron jobs
sudo su
echo <username> >> /etc/cron.allow
exit

#set cron
crontab crontab.<username>.file

#view to confirm
crontab -l
```

</article>

