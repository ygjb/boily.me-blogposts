Date: 2011-12-14
Title: Securing Browserid
Category: Mozilla
Tags: Persona, Identity, Security, Crossposts
Author: Yvan Boily 

*This post is cross-posted from the [Mozilla Web Application Security](https://blog.mozilla.org/webappsec/2011/12/14/securing-browserid) blog.*

One of the important projects that Mozilla has been building  in 2011 is BrowserID, a user-centric identity protocol and authentication service.  Significant work has gone into building out and testing the infrastructure and protocol to make sure that it is a robust, open, and simple to adopt authentication scheme.  If you want to learn more about BrowserID, [here is a quick 12 minute video](http://vimeo.com/32380595) that explains what it is, and why we are doing this.

BrowserID continues to evolve as we build support for it across Mozilla properties and encourage adoption from 3rd parties.  To date there almost 1000 different websites that rely on BrowserID, but we still have a long way to go to see large scale adoption!

Much of the effort we have put into reviewing the protocol and implementation of BrowserID is discussed in a recent presentation, a recording of which can be found below:

<iframe width="640" height="360" src="https://www.youtube.com/embed/rjdJvoWl-gk?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

[Slides: [html](https://people.mozilla.com/~yboily/browserid/) | [html(zip)](https://people.mozilla.com/~yboily/browserid_secreview.zip) | [pdf](https://people.mozilla.com/~yboily/browserid_secreview.pdf)]
(if the video doesn’t appear, click here!)

In addition to ongoing application and infrastructure security work in the next year, we are aiming for two significant milestones in 2012.  First we will engage two third party security reviews of the Browserid.org site, and the cryptography used in BrowserID (including the protocol, the algorithms used, and the libraries we are relying on).  Our objective in doing the third party review is to remain as transparent as possible in the development and review of the security aspects of BrowserID.  This commitment to transparency includes:

* opening up currently closed security bugs as the issues are resolved
* publishing the results of the 3rd party review once high risk issues are addressed

As we proceed with this effort we will publish additional information on this blog, and we will work to keep the community up to date at each stage of progress.

Second, once we have completed the 3rd party review, resolved the issues identified, and published the results, BrowserID.org will become one of the properties fully covered by the [Bug Bounty program](http://www.mozilla.org/security/bug-bounty-faq-webapp.html) (as always, exception bugs reported for none covered sites will be considered for bounty nomination).
