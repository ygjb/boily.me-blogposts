Date: 2011-02-08 
Title: Scaling Security
Category: Mozilla
Tags: Community, Security, Crossposts
Author: Yvan Boily 

*This post is cross-posted from the [Mozilla Web Application Security](https://blog.mozilla.org/webappsec/2011/02/08/scaling-security/) blog.*

The AppSec space is an extremely challenging field to work in, largely due to asymmetry; when you play defence you have to work to stay on top of each emerging threat, vulnerability, and development that falls into your scope.  Working to protect a system or application where there is fixed number of resources to spend on protecting a set of assets, choices have to be made about how to best spend those resources to prevent the attackers from winning.  The best way to do that is by applying risk analysis techniques and focusing on the highest risk assets.  Once those assets are identified, a decision has to be made about how to invest time and effort in design vs. implementation, static vs. dynamic analysis, and automated vs. manual testing.  Regardless of the goal of continuous engagement within the SDLC, decisions are made based on the risk and the pool of limited resources must be split up to work towards a solid defence.

The biggest challenge is that we have a rapidly growing development community; while the security team is growing to meet our needs, we need to find better ways to scale testing and analysis to get the same results with better efficiency.  Out of the gate, I am going to deal with one important issue by casually tossing it off to the side.  Tooling is a really important part of the discussion, but the bottom line is that tools won’t make a difference in your organization if you don’t have the right people to use them.  Good tools might help unskilled workers get good results, but skilled workers with suboptimal tools will still get great results.  The adage “It’s a poor craftsman who blames his tools” sums it up neatly.

In order to scale up a team with limited resources (time, people, money), there are a number of things that can be done.

* Threat Modeling/SDL activities are the best investment; you can fix many problems early, and eliminate extremely costly design weaknesses
* Bug Bounties  are a great way to reward the efforts of community contributors, but many contributions don’t come until the target is in production (i.e. the worst time to find bugs)
* Automated tools for dynamic and static analysis allow you to trade time and money for results, but you still have to invest in the people to use them properly
* Manual analysis consumes time and people; it takes a great deal of time and effort by skilled people to fix the problems
* Training and Education requires investment of time, people, and money, and although valuable, is rarely as effective as working through threat modelling and SDL activities with your development team

Each of these types of activities are already in place in Mozilla, but there is still more we can do.  We perform a great deal of manual testing because once we have reached that point in the development life cycle, it is the best way to find implementation or design issues that slipped through the cracks.   One area we are investigating is how to make our manual testing and analysis repeatable and reusable.

Some things we plan to do to move in this direction include:

* Building repeatable security test cases using tools like [MozMill](https://developer.mozilla.org/en/Mozmill), [Selenium](http://seleniumhq.org/), etc. where possible, and develop highly specific, but reusable guidance where it isn’t.
* Run repeatable test cases as regression testing against apps in development and production
* Identify high risk applications, frameworks, and components, and regularly review changes to them outside of releases and milestones
* Investigate how to use static and dynamic analysis tools to supplement regression and manual testing to bring the best value

As we get these activities up and running, we will keep the community updated on how we are progressing.

