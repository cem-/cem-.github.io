<article markdown="1">

<header markdown="1">
 
# Certificate Authorities, the problem is in the app

<time class="pubdate" datetime="2011-11-19">2011-11-19</time>

</header>

If you remember a few years ago, moxie was able to go grab a few wildcard certs, good for any domain (*, *.com, *.*.com, etc...), they were revoked, so he figured out a way to confuse the client into not checking for revocation (by sending a spoofed 'busy, please wait' signal back to the client). But, now it seems that at least one of those revoked certs has been allowed to be renewed via poorly written CA software. Now, he once again has a nice wildcard cert available for use.

  <blockquote><p><a target="_blank" href="https://twitter.com/jchillerup">@jchillerup</a> I dunno, but a CA recently sent me a renewal notice for expiring (revoked) null-prefix certs. I clicked, they renewed.</p>&mdash; Moxie Marlinspike (@moxie) <a target="_blank" href="https://twitter.com/moxie/status/137976502498242560">November 19, 2011</a></blockquote>

This isn't the first sign of poor CA web apps that were written to ease the load on persons running the CAs, or on the people requesting the certificates. You can tell that the so named, 'ComodoHacker' that procured certs for DigiNotar and the Comodo subsidiary used a flaw in the web app. If you look at the private keys that he generated, they have the extra tidbits that CAs inject into the certs Distinguished Name, as well as the revocation server data. If you wanted to steal a cert, wouldn't want it to be un-revoke-able by leaving out any valid revocation information? Would you not want to leave out the unique identifier that allows one looking at the DN to see it was a DigiNotar cert?

CAs either need to really work on shoring up their webapps, or the CA Browser Forum needs to revoke their approval status due to use of vulnerable webapps. (This approval would come from the CAs paying for vulnerability tests with an internal and external perview)

</article>
