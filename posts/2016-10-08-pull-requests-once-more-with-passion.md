# Pull Requests: Once More with Passion

At OurHealth this week, one of our engineers, Corin, was working on our upcoming online scheduling feature. We have been mostly backend focused for the last couple months, but got a great new design from our partner [Innovatemap](http://innovatemap.com/) and decided to refine our design implementation process. We've had many discussions about [atomic design](http://bradfrost.com/blog/post/atomic-web-design/) in the past and thought this project would be a good chance to implement it from scratch. To help us iterate rapidly, we decided to introduce [react-storybook](https://getstorybook.io/) as well. Corin went off for a few days, typing feverishly and leveling up his CSS skills, then came back with a pull request. A big one.

We have a general rule at OurHealth that pull requests should be as small as possible. Small pull requests make it easy for reviewers to load the full context of the problem into their head and provide good feedback along the way. It will be easier to see the shape of an algorithm or the relationships between classes. If you've ever reviewed an enormous pull request, you know that about 20 minutes in your comment quality starts to suffer, and by the end you're not just skimming to get it over with. (Dark pattern: If you ever need to sneak anything into a code base, hide it in a giant, dense pull request with lots of unrelated changes.)

Corin's pull request was perfectly reasonable, but it seemed to conflate a few different things:

1. Introduce react-storybook and prove that it would be a good foundation for design work
2. Prototype some atomic design primitives (atoms, molecules) and convince us of the approach
3. Build the design language once we agreed on direction
4. Use the design language to implement scheduling

The single giant pull request made it hard to tease apart these threads. I was jumping between react-storybook configuration code, generic design atoms, and domain-specific scheduling code. Some of the atoms seemed prematurely abstracted, but by rejecting some of these atoms I was rejecting the entire pull request, 90% of which made our code base immediately better.

In this case, we decided to keep the pull request as-is and move forward, but it got me thinking: how can we use pull requests not just to document the mechanics of a change, but to tell a story, make a case, or build consensus? Most fiction writers have internalized the old adage "Show, don't tell." I think we can use pull requests to do the same thing. Instead of setting up a meeting to debate build tools, do a quick spike like this one I did for an [Indy.js talk](https://github.com/shipstar/js-packaging) and let people weigh in on something concrete. If you think Redux would help you manage client-side state better, take an afternoon to introduce it to a small part of your application, then submit a pull request and ask "What do you think? Should I keep going?"

The next time you're about to submit a pull request, take a step back and ask yourself:

1. What is the goal of this pull request?
2. What context can I provide to the reviewer to make their life easier?
3. Does this pull request help explain why we're making the decisions we made in case it comes up a year from now?

If we're more thoughtful about using pull requests as communication tools, we'll make better decisions and ship better software, all while having fewer meetings.

P.S. If you like writing great code and even better pull requests, [we're hiring](https://www.ourhealth.org/about-us/careers/#jobs)!
