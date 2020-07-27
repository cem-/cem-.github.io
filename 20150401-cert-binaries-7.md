<article markdown="1">

<header markdown="1">
 
# Certificate Binary Posters (Part Seven)

<time class="pubdate" datetime="2015-04-02">2015-04-02</time>

</header>

<p>Certificate revocation has been done in two primary ways Certificate Revocation Lists (CRLs) and the Online Certificate Status Protocol (OCSP) at least until some browsers <a href="https://www.imperialviolet.org/2014/04/19/revchecking.html" target="_blank">stopped</a> checking for revocation. However, extended validation (EV) certificates still elicit active revocation checking by most browsers.</p>

<p>CRLs are a list of revoked certificate serial numbers from a given certificate authority. Besides the serial number, the revoked certificate list includes the timestamp of the revocation occurrence and the reason the certificate was revoked (though the reason is <a href="http://www.ccs.neu.edu/home/cbw/pdf/imc254-zhang.pdf" target="_blank">not always useful</a> in the real world). This poster has only one revoked certificate for brevity, however, if there were others they would be listed serially within the revokedCertificatesList section.</p>

<a href="/art/cryptoposters/crl.png" target="_blank"><img src="/art/cryptoposters/crl.png" alt="CRL" /></a>

<p>When in normal operation certificate authorities have CRL sizes that can get quite large. After <a href="http://en.wikipedia.org/wiki/Heartbleed" target="_blank">heartbleed</a> the CRL for the main CA used by CloudFlare was nearly five megabytes and used up nearly $400K worth of bandwidth. On the other hand, OCSP is much less weighty when compared to CRLs. Also, OCSP has the ability of being able to be used as a type of whitelist rather than a blacklist like CRL. An OCSP server is able to affirmatively acknowledge that a certificate is valid. With OCSP, you get a simple request and response for only the certificate you are checking rather than a large file which the validator must search through checking every serial revoked by the CA. The OCSP request is built first from the validating side by issuing a request of the OCSP server (specifying that by hashes of the CA name and key) for a particular serial.
</p>

<a href="/art/cryptoposters/ocspReq.png" target="_blank"><img src="/art/cryptoposters/ocspReq.png" alt="OCSP Req" /></a>

<p>The OCSP server will reply back with a response: good, revoked, or unknown. Alternatively, the server can return unauthenticated error codes: malformed request, internal server error, try again later, client signature required, or unauthorized. This response is split into 3 main sections, the wrapper information, the response from the server, the signature, and the chain of the OCSP responder. The server response first contains the responder subject name information, the time the response was signed, and the response. The response is made up of the information from the request, the response (good, revoked [with the time and reason code], or unknown), and the time the response is good from followed by an optional end time for the response.</p>

<a href="/art/cryptoposters/ocspResp.png" target="_blank"><img src="/art/cryptoposters/ocspResp.png" alt="OCSP Resp" /></a>

<p>These methods have largely been replaced by Certificate Trust Lists (CTLs) in Microsoft and CRLSets in Chrome (and soon <a href="https://blog.mozilla.org/security/2015/03/03/revoking-intermediate-certificates-introducing-onecrl/" target="_blank">OneCRL</a> in Firefox &gt;v37. However, these only typically cover emergencies or Issuer/CA certificates. The real solution is short term certificates (certificates only good for a day or two). If that is not feasible, then the solution is requiring servers to <a href="https://tools.ietf.org/html/draft-hallambaker-muststaple-00" target="_blank">staple OCSP responses</a> within the TLS handshake, forcing valid up-to-date revocation information in every connection.</p>

</article>
