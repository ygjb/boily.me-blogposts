Date: 2011-10-26
Title: Automating Test Cases
Category: Mozilla 
Tags: Security, Tools, Crossposts
Author: Yvan Boily

*This post is cross-posted from the [Mozilla Web Application Security](https://blog.mozilla.org/webappsec/2011/10/26/automating-test-cases/) blog.*



Earlier this year I wrote about some of the challenges of scaling security efforts in an organization, and I mentioned that we are working to adopt better tooling to assist us in this.  We have been working towards improving security in the development lifecycle by making security tests a part of the quality assurance process. In order to accomplish this we worked with the QA team at Mozilla to create a simple tool called Garmr to integrate automated security test cases as part of our continuous integration (CI) processes.

When we started the discussion about which tools to use, our requirements were pretty straightforward; it needed to be fast, simple, and accurate.  When we looked at Selenium and Mozmill the feedback we got from other teams is that although powerful, these frameworks were complex to configure properly, and had significant overhead to maintain as a project progresses.  Since the focus was on testing web applications in a repeatable fashion, we identified a set of required functionality and David Burns from the very awesome Mozilla QA team put together the Garmr prototype and initial test cases.

Garmr has been public since its initial version, but the tool has now reached the point where we will start to leverage it in our testing and CI processes.  The tool works by running a series of tests against target URLs and reporting back the results.  The results are currently formatted as a JUnit style XML report that can be consumed by other tools such as Jenkins.

## Garmr Test Cases

Garmr currently supports two types of test cases that can be authored, an Active Test and a Passive Test.  ActiveTests are expected to make at least one HTTP request, and return the most relevant HTTP response after the check is completed.

Here is an example of an ActiveTest that makes a simple HTTP GET request:

	class WebTouch(ActiveTest):
	    run_passives = True
	    description = "Make a GET request to the specified URL, and check for a 200 response after resolving redirects."
	    def do_test(self, url):
	        response = requests.get(url)
	        if response.status_code == 200:
	            result = self.result("Pass", "The request returned an HTTP 200 response.", None)
	        else:
	            result = self.result("Fail", "The response code was %s" % response.status_code, None)
	        return (result, response)

The test case makes an HTTP Get request, and passes or fails dependent on the response code.  This very basic check does serve a purpose; it grabs an HTTP response to run passive tests against.  For an example of a more complex check, look at the StsUpgradeCheck implemented in the [corechecks](https://github.com/ygjb/Garmr/blob/master/Garmr/corechecks.py) module.

PassiveTest instances receive a copy of an HTTP response and analyze it to determine if the test passes or fails.  In most circumstances, Garmr will run all of the configured PassiveTests against the result of each ActiveTest.  The goal of a passive test is to inspect each the response of a query for properties that are expected from a secure web application.

This is an example of a passive test that checks an HTTP response for the presence of X-Frame-Options headers:

	class XFrameOptionsPresent(PassiveTest):
	    description = "Check if X-Frame-Options header is present."
	    def analyze(self, response):
	        xfoheader = "X-Frame-Options"
	        xfo = xfoheader in response.headers
	        if xfo == False:
	            result = self.result("Fail", "X-Frame-Options header not found.", None)
	        else:
	            result = self.result("Pass", "X-Frame-Options header present.", response.headers[xfoheader])
	        return result

The goal is to allow developers to create test cases that are specific to their applications and gain the benefit of running pedantic checks for security related attributes such as cookies and headers each step of the way.  Note that there is no practical limitation on what a passive check does, as long as the result object is returned properly.

## Using Garmr

The current version of Garmr can be downloaded from the [Garmr Github repository](https://github.com/mozilla/Garmr).

Getting, installing, and using Garmr is very easy:

	git clone https://github.com/mozilla/Garmr.git
	cd Garmr
	sudo python setup.py install
	garmr -u http://my.target.app

## Limitations

Garmr is an alpha tool.  The only part of it that we expect to remain stable at this point is the Xml Report format that it produces, since this is specified by the Jenkins tool chain that we are integrating with.

This tool is not intended to replace a typical dynamic or static analysis tool any more than the existence of Unit Tests replaces end to end functional testing, but it does provide a simple facility for QA, development, and security teams to collaborate on web application testing.

Currently the tool can be used to run a number of simple tests, and supports the ability to load modules; two examples of how a module would be written are included in djangochecks.py and webchecks.py

There is a list of features still to come:

* less noisy CLI
* proxy support (already supported in requests)
* sessions (controlled; sequence for active tests, with a cookie jar that is propagated through the session)
* detailed reporting, including the ability to record all HTTP requests and responses generated
* the ability to filter which passive checks are run by check name or by check type (i.e. cookies, headers, content-type, etc)
* support for additional protocols (websockets, spdy)
* Implement instances of each test case for each target scanned to allow them to retain state as a set of tests progresses.

I am very excited to see how the tool will develop over the next few months as we have an intern who will be working to implement these and other features, so please test it out, give us feedback (patches and feature requests are welcome too!).
