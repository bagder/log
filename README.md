# Daniel's weekly report

# June 10, 2022

## Happened this week

### prev week

I never sent a weekly report last week because I got crazily busy arranging my
daughter's graduation so I had to optimize away that part on the Friday. Then
I got struck down by covid and decided to skip it completely for that week.

### curl up

On Monday this week, we were supposed to have had the curl up conference in
San Francisco, but we had to cancel. When I was about to fly out of Sweden on
Saturday I had to do a mandatory last minute covid-19 test, and to my shoock
it came back positive so I was effectively grounded and prevented from travel.
Terribly unfortunate, but we aim at doing an all-virtual version instead in
September. Stay tuned for the exact date.

A few Europeans of course had already taken off by the time I canceled the
event, which was deeply unfortunate but the curl project will still reimburse
them for their travel so at least not a direct financial hit for them. I
apologize!

I am now almost entirely back on my feet again.

### websockets

I have started taking the first baby steps on the journey to [WebSockets
support](https://github.com/curl/curl/wiki/WebSockets) in curl. There is a
dedicated sponsor behind this, but I will let them break the news about who
they are when they feel ready.

I have already faced some disappointments and had to do some replanning as the
library I planned to base this implementation on just does not seem to be
suitable.

I might try to get some live-streamed hacking on websockets going in the
coming weeks.

### survey

The user survey ended mid last week but it has been a busy period and while I
have slowely been crunching the data in the background, it is going to take me
a while longer until I can present the results and analysis from the survey.

It is however yet again striking how similar people answer the questions year
by year!

### feature freeze

No more features will be accepted into curl before the pending next
release. That is what feature freeze means and we typically have it frozen for
the later half of the release cycle to keep us focused on bug-fixing and
polish on the sprint towards release.

### release date moved

I announced a slightly adjusted release date for curl 7.84.0: **July 1st
2022**. Due to me organizing some personal travels I decided it would work
smoother to do the release a few days earlier than previously planned.

### security

OpenSSF is sponsoring a **curl security audit** that we will run with the help
of OSTIF. The work of finding a suitable auditor company/orgnization has
kicked off and in a few weeks we will know who will get assigned the project.

In the mean time, security researcher extraordinaire Harry Sintonen submitted
no less than four new security issues to the project that have been registered
as CVEs and will be announced and revealed in assocation with the pending
release. (Harry is now the name behind no less than **17** curl CVEs.)

I have assisted the Apache Security team, sharing my view and knowledge about
some specific protocol related questions with a security angle.

## Blog posts

- [Making libcurl init more thread-safe](https://daniel.haxx.se/blog/2022/06/08/making-libcurl-init-more-thread-safe/)
- [New HTTP core specs](https://daniel.haxx.se/blog/2022/06/06/new-http-core-specs/)

## Coming up

- podcast participation on Monday
- continued work on WebSockets
- survey analysis
- crossing my fingers for new port of tiny-curl
- ocsp go ahead?

# Older weekly reports

- [May 2022](May-2022.md)
- [April 2022](April-2022.md)
- [March 2022](March-2022.md)
- [February 2022](February-2022.md)
- [January 2022](January-2022.md)
- [December 2021](December-2021.md)
- [November 2021](November-2021.md)
- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
