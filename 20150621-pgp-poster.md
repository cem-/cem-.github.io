<article markdown="1">

<header markdown="1">
 
# PGP Public Key

<time class="pubdate" datetime="2015-06-21">2015-06-21</time>

</header>

Pretty Good Privacy (PGP) has been around since 1991, it has since gained notoriety and ubiquity as one of the most popular<sup>[citation needed]</sup> person to person publication privacy programs. Now <a href="https://keybase.io/cem_">keybase.io</a> and even <a href="https://www.facebook.com/notes/protecting-the-graph/securing-email-communications-from-facebook/1611941762379302">Facebook</a> are allowing users to receive encrypted communications from their systems, whether or not that is a <a href="http://blog.cryptographyengineering.com/2014/08/whats-matter-with-pgp.html">good idea</a>.

After learning about the ins and outs of <a href="https://www.cem.me/pki/index.html">certificate structures</a>, I tuned to PGP to learn how they are put together. Some of it is quite elegant, and allows the format to save space, especially in the packet headers where 2 bytes can convey essentially the same information that take 6 bytes in <a href="https://www.cem.me/20150209-cert-binaries-4.html">x.509</a>. PGP keys are made up of these packets, each packet is used to convey information about the key as a whole. By default, a key has 5 packets; Public Key (for signing), User ID (just text), Signature packet (times, algorithms, settings, and the Signature [over the Public Key, User ID, and most of the signature packet]), sub-key (for encrypting), and the sub-key signature.

Each header starts with a 8-bit value. The first bit is always set, the second is a switch between old and new packet styles (the new style is used for tag types represented by values larger than 4 bits, by default, keys just have old style), for the old style bits 3 through 6 indicate the <a href="https://tools.ietf.org/html/rfc4880#section-4.3">packet type</a>, the last 2 bits tell the number of length bits that immediately follow the header packet.

The public key packet contains the signing data and certifying other’s keys, the key for encrypting the data is the sub-key. The User ID packet is just UTF-8 data, this is normally a name, email address, and a comment from the owner (there is quite a bit of room here to store data... make sure you subscribe with <a href='http://cloud.feedly.com/#subscription%2Ffeed%2Fhttp%3A%2F%2Fwww.cem.me%2Fcem.rss'>feedly</a>, or with <a href="https://www.cem.me/cem.rss">rss here</a>). The two signature packets are used to show binding between a held private key by signing the hash of the public key in the particular packet (key or sub-key), and the information specified in the signature packet. Within the signature packet, there are several <a href="https://tools.ietf.org/html/rfc4880#section-5.2.3.1">sub-packets</a> that can contain a multitude of data from signature time policy data like what the key should be used for. This data is encoded in various ways from actual integer values, to hexadecimal values denoting particular values, and binary values where each bit adds a new flag value.

Here is a posterized PGP key, it uses RSA keys (only 1024-bit for brevity) for both signing and encrypting and has an expiration date, the other values are just the OpenPGP defaults.

<a href="http://www.redbubble.com/people/cem-/works/15307088-pgp-public-key?c=377869-pki-posters" target="_blank">You can get a copy printed out here</a>

<a href="https://www.dropbox.com/s/57jc0f3s9myezwu/PGP_Pub.png?dl=0" target="_blank"><img src="https://lh3.googleusercontent.com/-JeDlyJY4fc8/VYpFna9YeMI/AAAAAAAAGwQ/_ySxho-jhwM/s800/PGP_Pub.png" alt="PGP Public Key" /></a>

</article>
