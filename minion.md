Date: 2012-11-05
Title: Minion - Why, What, and How
Category: Security
Tags: Minion, Mozilla, Tools
Slug: minion-why-what-how
Author: Yvan Boily
Summary: An explanation of Minion and why I think it is important.

Once we get where we want to with Minion, we will talk more about what we plan to do with it within Mozilla, both through a public webcast, and on the Mozilla Security blog, but right now we just aren't ready for it.  Instead, I will explain Minion, and lay out my personal goals for the project.

##Why
At Mozilla I work with a team of really bright people who are working hard on some of the challenges of building secure software and managing the IT security related risks associated with a high-profile open source project.  One of the biggest challenges we face is that Mozilla is a public benefit organization; this means that we don't tend to drive the same scale of insane profits that some of our competitors do (and profits aren't bad thing!), which means that we have to find new and interesting ways to scale; I spoke about some of these things at AppSecUSA at the end of October, and the video should be available online soon.

Adding to this challenge is the state of the Application Security workforce.  For skilled AppSec people, the unemployment rate is essentially 0%.  For under-skilled[1] AppSec people, it is not much higher; this provides the challenge of trying to recruit skilled, knowledgeable people to help with some of our activities.  We have had a huge amount of success over the last two years in growing and building an effective team, but like every other security team, we are increasingly competing for a small number of high value individuals.  (Hey, interested in applying for jobs?  Look [here](http://careers.mozilla.org/en-US/)!)

To even further complicate matters the amount of competition in the security space, and the history of the security community telling everyone that security sucks, security is hard, and they aren't smart enough to get security right, have all contributed to the proliferation of Security As a Service vendors.  Unless you have a huge amount of financial resources, compelling and interesting problems to work on, or some other incentive, it is very difficult to attract security talent when vendors are offering top dollar for people to work in their bug mills (again, not a bad thing; good quality teams are expensive, and vendors can help offer access to good talent).

##What
For the last year I have been preaching automation to our team, and last spring we started growing our Security Automation Engineering team.  Following that, we recently started to build out a new team to focus on developer oriented tools.  We wanted an "security tool automation system".  We envision a tool that will provide basic automation for a range of security tools, with intelligently selected configurations for ease of use, and well thought out configuration options to allow the user to configure a range of tools by modifying a small set of values.  This tool is called Minion.

Minion is intended to be disruptive. 

First, it will help us break out of the pattern of running and using security tools within our team; we want all of the developers in our organization to use them.  We want our developers to do horrible things to the applications and services they write, and we want it to be as easy as the push of a button.  If my team is asked to review an application[2] for release to production, having passed through Minion should be one of the first steps.

Second, we want Minion to become a Security As A Service platform.  Automation is not the answer to everything; In the long term, Minion should provide a solid toolkit that any security team can use to organize around.  Once we finish the core feature set of Minion, we will start to focus on the team oriented aspects of the platform.  It should be easy to extend, easy to adopt, and support hooking into each step of the SDLC.  In short, we want to create a platform that allows any good security team to compete with the established Security As A Service players in terms of service delivery, documentation, and workflow, without constraining people to a specific philosophy or process.

Finally, we want Minion to be a framework.  As an information gathering tool, it is effectively useless if that information feeds into a write-only repository.  To that end we are working to define clear, extensible formats that can be used to integrate with and consume data from Minion.  Want to create a fancy dashboard for C-Level executives?  Minion should allow that.  Want to write a module to automate generating a report worthy of a typical audit firm?  Minion should allow you to do that!  Want to perform data mining to find out vulnerabilities that are most common in the applications you test?  Minion should allow that!  By building Minion around REST APIs and modern web standards, it is possible to build any kind of mashup you can think of with the data that Minion collects and the results it tracks.

##How
I pushed for Minion to be created, but it would still be a poorly written set of PoC scripts if it wasn't for the hard work of [Matthew Fuller](https://twitter.com/matthewdfuller), [Simon Bennetts](https://twitter.com/psiinon), and [Stefan Arentz](https://twitter.com/satefan).  These guys have done an amazing job, and I look forward to seeing how they continue to push the project forward!  If you are interested in Minion, you can check out the repo, or join the mailing list using the links below!

* [Minion on Github](https://github.com/ygjb/minion)
* [Minion Developer Mailing List](http://groups.google.com/group/mozilla-minion-dev) 
* Or join us on #minion on [irc.mozilla.org](https://irc.mozilla.org)

Thanks for reading!

Yvan

[1] "Underskilled": Securing web applications is hard.  Securing applications is hard.  Securing applications that people use to build web applications and access web applications is really hard.  Not everyone is cut out for the job, and there is nothing wrong with that; there are a lot of opportunities for people that don't demand staying on the bleeding edge of technology.

[2] Note that this is different from the consultative security work we do over the course of a project; Minion is not a substitute for a security program, it simply offloads some of the testing burden to automated tools and lays a foundation that the security team can look at when starting a final review before a product or service is released.
