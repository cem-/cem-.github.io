<article markdown="1">

<header markdown="1">
 
# Certificate Binary Posters (Part Six)

<time class="pubdate" datetime="2015-03-15">2015-03-15</time>

</header>

<p>One thing that is <a href="20141221-cert-binaries.html">noticeably</a>, <a href="20150104-cert-binaries-2.html">different</a>, <a href="20150121-cert-binaries-3.html">from</a>, <a href="20150209-cert-binaries-4.html">previous</a>, <a href="20150301-cert-binaries-5.html">posters</a> is that these formats are not encoded in base64, they are binary files. Most of the other files can be interpreted by cryptosystems in both binary and base64, and we typically transport them by first encoding them in base64.</p>
<p>In these formats, in order to show the binary in a visual representation I used <a href="https://en.wikipedia.org/wiki/Netpbm_format#PGM_example">Netpbm</a> (<b>Net</b>work <b>p</b>ortable <b>b</b>itmap for<b>m</b>at) with the PGM (<b>P</b>ortable <b>G</b>ray<b>m</b>ap) format to translate the hexadecimal values into a format easier for humans to visualize. (A more fun format would be to <a href="https://gist.github.com/windytan/7910910/">use emoji</a>, but that would not fit quite as well with the rest of the poster).</p>
<img src="art/emoji.png" alt="emoji pfx" />vs<img src="art/pgm.png" alt="pgm jks" />
<p>Microsoft came up with the pfx format (which was later changed slightly and reworked as PKCS &#35;12), and recieved <a href="https://www.cs.auckland.ac.nz/~pgut001/pubs/pfx.html">much criticism</a> due to the complex nature, terminology, and internal formats. At first glance the p12 format seems to be fairly complex, it includes many wrappers of wrappers that enclose keys, certificates, and descriptive data. The reason for all of those is that pfx files can contain (according to Gutmann), "CRL's, keys, names, cookie recipes, dirty laundry, spare lightbulbs, and the kitchen sink". However, for storing certificates and a private key in pfx, it is really just a list of pairs of encrypted certificate chain and the associated encrypted key. </p>
<p>The keys and certificates in the pfx are stored in separate containers and encrypted with different keys and most of the time different algorithms also.</p>
<p>When using Windows, there really is no way around the algorithm used. The default is to encrypt the certificates with RC2 and the private key with 3DES, this means that the highest strength you would ever be able to achieve is equivalent to 3DES. However, on OpenSSL, you can specify the encryption algorithm for both the key and the certificates to use the stronger AES-256 by adding additional flags:<br />
<code>-certpbe AES-256-CBC -keypbe AES-256-CBC</code></p>
<p>Of course, at the moment, the strength is predominantly up to the password used as the best way to defeat even the Windows version is to use a password list. This is somewhat slowed by the number of rounds the key derivation algorithm is passed through; 2000 on pfx files generated via Windows and 2048 by default from OpenSSL.</p>

<a href="art/cryptoposters/p12.png" target="_blank"><img src="art/cryptoposters/p12.png" alt="pfx"/></a>

<p>Java has its own proprietary format that it named JKS, which stands for Java KeyStore.</p> <p>While the p12 format is binary encoded ASN.1, jks format files are a strange mix of binary and ASN.1. The file begins with a "magic number" as <a href="http://en.wikipedia.org/wiki/List_of_file_signatures">many other</a> binary files do. After that comes a list of different keys or certificates. JKS files are also quite extensible and are able to hold many objects, including lists of chains, certificates, roots, as well as lone private keys. The number of keystore entries is defined at the beginning of the file and the data is listed in a serialized manner. For this example of just an x.509 certificate and key, the entry contains: a plaintext alias, encrypted private key, and plaintext chain.</p>
<p>Unlike pkcs12, you cannot choose the algorithm used to protect the keys, so everyone is stuck with a proprietary implementation of a password based key derivation scheme using MD5 to create a 3DES key. </p>

<a href="art/cryptoposters/jks.png" target="_blank"><img src="art/cryptoposters/jks.png" alt="jks" /></a>

<p>The moral of the story, is use a long and complex password for either of these formats. Even so, if your keystore does get out, you will need to revoke your certificate. More on that next post.</p>

</article>
