<article markdown="1">

<header markdown="1">
 
# Training Users to Be More Secure
<time class="pubdate" datetime="2013-10-28">2013-10-28</time>

</header>

One of the things that a corporation, website, or mobile application should do, is in all of its interactions with the users of its services insure that none of the actions that it requests or requires would be something that in a malicious context would compromise the security those users.

You should not do things like: have users enter credentials over a non-SSL log-in screen, force users to click through an invalid certificate to get to your site, or use a pseudo-public piece of data for a password (e.g. SSN or birthday).

Last week, LinkedIn broke the rule of not requiring the user to engage in risky behavior. The service <a target="_blank" href="http://engineering.linkedin.com/mobile/linkedin-intro-doing-impossible-ios">Intro</a> is described as a <a target="_blank" href="http://blogs.csoonline.com/application-security/2808/linkedin-intro-data-meet-security-issues">bad idea</a> by Dave Lewis <a target="_blank" href="http://threatpost.com/linkedin-intro-app-equivalent-to-man-in-the-middle-attack-experts/">and</a> <a target="_blank" href="http://bits.blogs.nytimes.com/2013/10/24/linkedins-new-mobile-app-called-a-dream-for-attackers/">others</a>, was <a target="_blank" href="http://blog.linkedin.com/2013/10/26/the-facts-about-linkedin-intro/">rebutted</a> by a LinkedIn security manager which sparked a reply by Martin McKeay. Up to now, I have seen many people talking about how bad an idea the system is as a whole, so I will not rehash that part. Instead, I want to focus on the _how_ not the what.

Which brings me back to forcing users to engage in risky behavior. The way that you 'install' Intro, is to first, go to the Intro website rather than the app store. One of iOS's most lauded features is that it is kept more secure only allowing apps from the app store. Getting an app or 'app' from elsewhere should raise red flags.

Next, you enter in your Gmail/iCloud/Yahoo/AOL/etc. email password, on LinkedIn's site. You should not enter your password for one site on another. It is reasonable for sites to want functionality that would normally need other sites credentials, but this is why things like <a target="_blank" href="http://en.wikipedia.org/wiki/OAuth">oAuth</a> and <a target="_blank" href="http://en.wikipedia.org/wiki/SAML_2.0">SAML</a> were created.

Next, you are required to install a <a target="_blank" href="https://developer.apple.com/library/ios/featuredarticles/iPhoneConfigurationProfileRef/">configuration profile</a>. Configuration profiles very useful for giving corporations access to a phone. As <a target="_blank" href="http://www.bishopfox.com/blog/2013/10/linkedin-intro/">Bishop Fox said</a>, "A profile can be used to wipe your phone, install applications, delete applications, restrict functionality, and a whole heap of other things". Users should only install these profiles if they truly understand what they do, or are required to by their company.

Also, using this method, there is a set of certificates installed by the mobile config profile. This is a further potential avenue for compromise in a malicious setting. Configuration profiles in iOS are powerful things, training users to install them can lead to making it a lot easier to pull off a social engineering trick, similar to what I described in my <a target="_blank" href="http://docs.google.com/viewer?a=v&pid=sites&srcid=Y2VtLm1lfGJsb2d8Z3g6N2E5YTM1YzllMTYxZDA3Mg">BSides San Antonio talk</a> (starting slide 26).

Make the Internet a better place: as a website/app/service provider you should choose an architecture using methods that propagate more secure, rather than risky, behavior.

Happy Cyber Security Awareness Month

-cem

</article>
