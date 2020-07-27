<article markdown="1">

<header markdown="1">
 
# Certificate Pinning

<time class="pubdate" datetime="2012-12-01">2012-12-01</time>

</header>

Today I created a webapp that allows for sysadmins and security savvy chrome users to add certificate pins to their sites and browser.

Give it a try over at <a target="_blank" href="https://certpins.appspot.com/">https://certpins.appspot.com/</a>.

Certificate pinning is a way to tell clients what cert or CA they should be seeing when they connect to your website. The tool builds upon the go implementation of cert pinning in the key-pinning draft.

<u>Resources:</u>

Current Draft Key Pinning

<a target="_blank" href="http://tools.ietf.org/html/draft-ietf-websec-key-pinning">http://tools.ietf.org/html/draft-ietf-websec-key-pinning</a>

Adam Langley's Blog Post (where I first learned about pinning certs)

<a target="_blank" href="https://www.imperialviolet.org/2011/05/04/pinning.html">https://www.imperialviolet.org/2011/05/04/pinning.html</a>

Moxie's post about why you should use key pinning in your mobile apps.

<a target="_blank" href="http://www.thoughtcrime.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/">http://www.thoughtcrime.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/</a>


The code is at <a target="_blank" href="https://github.com/cem-/certpins">github</a> for review and collaboration.


**EDIT:**

I've called this certificate pinning even though the process is key pinning because the app that creates the key pins specifically only takes certificates to make the pins. Regardless of semantics, enjoy the app for creating key pins.

</article>
