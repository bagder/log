# Daniel's weekly report

# June 17, 2022

## Happened this week

### websockets

The WebSockets work took off. Once I decided to not use a third party library
I proceeded and implemented the [first
steps](https://github.com/curl/curl/pull/8995). It can already do some basic
back and forth messages fine that I verified talking to a live test server.

In parallel with that start, I have to [introduce
`CURLOPT_PROTOCOLS_STR`](https://github.com/curl/curl/pull/8992) as a
replacement for `CURLOPT_PROTOCOLS` because when I add support for two new
protocols to libcurl the existing 32 bit protocol bitmask gets overflown - so
we need a new way to control which protocols to allow. A way that isn't
limited to 32 protocols.

Once some WebSockets basics worked, I started looking into the test server
issue and quickly decided I will write my own server implementation as well
and just extend the existing HTTP test server with it for maximum
flexibility. I started and I have one very basic test case working. It also
immediately stressed that my initial client side code is still too naive etc.

I've tried to update the WebSockets PR description with items that work and
things still not work. I will try to maintain that going forward, while also
slowly extending the documentation that is part of the PR.

I brought two separate WebSockets design questions to the curl mailing lists:

1. how should we [make the curl command line tool deal with websockets](https://curl.se/mail/archive-2022-06/0008.html) in the ideal way?
2. thoughts on the [write callback for websockets](https://curl.se/mail/lib-2022-06/0049.html)

My plan is to take this gently and slowly forward, as I also have other things
to work on at the same time. I believe I've managed to land some fundamental
parts already that I will work on improving and gluing in properly going
forward, supported by tests using my coming test server.

I'm also hoping for and assuming that I will get more guidance from users
during this progress to make sure this becomes exactly as good as we want it
to be. I'm aiming for a first implementation to land in the October 2022
release.

### REUSE

I merged the PR that brought REUSE compliance to curl and now we have better
control and information about licenses and copyright throughout the
project. (see separate blog post)

Max Mehl did most of the work for this but I'm pretty satisfied with the
follow-up cleanups I did as now we have scripts and decent infra to maintain
this state as well going forward.

### analysis

Putting together the user survey analysis always take quite some time and
effort to put together, write up and generate the graphs for, but I managed to
finally complete it this week. 36 pages for everyone to dig into. See blog
post.

### URLs

The subject of URLs vs URIs came up on the IETF HTTP Working group mailing
list and I could help but [to
respond](https://lists.w3.org/Archives/Public/ietf-http-wg/2022AprJun/0169.html). Short and sweet but with no intention to go full rant on this again.

### podcasts

I participated on one podcast on Monday and I had another preparation meeting
on Thursday about a coming podcast participation. I'll mention and link them
in future weekly reports when they go public.

## Blog posts

- [curl user survey 2022 analysis](https://daniel.haxx.se/blog/2022/06/16/curl-user-survey-2022-analysis/)
- [curl is REUSE compliant](https://daniel.haxx.se/blog/2022/06/17/curl-is-reuse-compliant/)

## Coming up

- WebSockets
- issue with h2 over HTTPS proxy
- OCSP?

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


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
