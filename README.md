# Daniel's weekly report

# September 9, 2022

## WebSockets

I have merged the first [WebSockets](https://curl.se/docs/websockets.html)
take into the curl master branch. You need to enable it explicitly in the
build to get it, but I hope lots of people do and try it out and give me
feedback.

There are several outstanding issues to do to make the WebSockets support
really good, but now at least this significant first step has been
taken. Thanks for flying curl.

[Corellium](https://twitter.com/CorelliumHQ/status/1539277242886500353)
sponsors my WebSockets work.

## talk

I did a talk called "rust in curl" for a local FOSS-sthlm meetup on Thursday.

## curl up 2022

[curl up 2022](https://github.com/curl/curl-up/wiki/2022) happens next week. I
have recorded my four presentations already and I will make them available for
viewing already early next week. I will also link to the slides.

## URL parser

My URL parser cleanup and speedup work was merged. It runs slightly faster,
with fewer and smaller mallocs using fewer lines of code.

As a side-effect of my polishing the URL parser, I decided to look into the
ctype functions we use in curl and I optimized them as well... when doing that
optimization I fell over and fixed two related issues: I found some leftover
use of the extern ctype funcitons and I also realized that curl was using
allowing control codes in far too many parsers when it should rather only
allow spaces and tabs.

Another side-effect of my adventures in the URL parser was the creation of the
`http://http://http://@http://http://?http://#http://` URL and [my
tweet](https://twitter.com/bagder/status/1567162794092404742) got an amazing
attention.

a side-effect of me cleaning up a lot of whitespace parsers, I broke a
critical function that parses numbers which triggered a OSS-fuzz report so I
got to work on that as well.

Domino effects are real.

## Blog posts

- [A bug that was 23 years old or not](https://daniel.haxx.se/blog/2022/09/05/a-bug-that-was-23-years-old-or-not/)
- [http://http://http://@http://http://?http://#http://](https://daniel.haxx.se/blog/2022/09/08/http-http-http-http-http-http-http/)

## Coming up

- code audit status meeting on Tuesday
- curl up 2022 on Thursday
- continued work on more WebSockets things

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# September 2, 2022

## curl up 2022

Less than two weeks left now! [curl up 2022](https://github.com/curl/curl-up/wiki/2022)

## Funding

This seems to be happening. Funded dedicated curl work. Terribly exciting and
I cannot wait to tell you all about it. Once everything is secured, signed and
stamped.

## Talks

I presume the summer and pandemic are over for real, as I suddenly received
several requests for keynotes and presentation later in the fall. I will do
some fun events for sure and talk curl, HTTP and open source in front of
audiences, but I am also not able to say yes to all requests I receive.

## Release

On Tuesday evening, the day before the release, I decided to check out a
rather mysterious CI job failure. The reason I had not looked at this CI
failure before was that this is one of the problematic CI services we use and
it frequently just has flaky CI jobs. False positives. But this time it was
not a false positive!

It took me a while to reproduce the problem locally and I submitted [an
issue](https://github.com/curl/curl/issues/9397) to the project in the early
evening, mostly to not make me forget about it. I then went to have family
time for a while and it was first when I got back to my computer later in the
night that it dawned on me that it was a rather silly regression problem I was
staring at. One that we really did not want to ship in the release the next
day.

After bisecting to the exact offending commit, it was a fairly quick thing to
spot the problem. Yikes, that was silly.

The time was around midnight when I submitted a
[pull-request](https://github.com/curl/curl/pull/9399) and the CI jobs started
to chew away on my fix. The CI jobs of course never run as slow as when you
are waiting for the results before being allowed to go to sleep...

At about 1 am in the morning the results were in for an enough number of CI
jobs that I was convinced the fix was good and would not break and burn
horribly. I could merge the PR and quickly head to bed.

The **curl 7.85.0** release went perfectly fine.

## URL parser

For no particular reason, I poked at the URL parser code in curl this week. I
spotted a way to reduce the size of the main handle for the API and then one
thing led to another and soon I had tweaked and polished the thing quite a
bit. To reduce memory allocations, simplify the code and ideally make it
faster. [The pull request](https://github.com/curl/curl/pull/9408).

Thankfully, we have quite a large number of tests for this functionality, so I
can be fairly sure I didn't break anything in a royal fashion.

It turned out surprisingly hard to speed up by more than just a little, but I
managed to reduce memory consumption significantly.

A casual reader might wonder why a URL parser has to do a lot of memory
allocations to begin with, but the reason is this parser stores all URL
components as separately allocated pointers for later easy and quick
access. Also: a URL can be extremely long and curl cannot keep that large
temporary buffers on the stack.

Even on my old machine with code built in debug mode, the code parses an
"average URL" in less than a microsecond. I think it is decent. (Average URL
being the average time for a few hundred different URLs I throw at it in my
simple performance tests.)

## Kodsnack

[Kodsnack 488](https://kodsnack.se/488/) went public. A podcast episode
recording I participated in last week - speaking Swedish. We discussed open
source maintenance and a lot of details that entails with a few other fellow
open source maintainers.

## Security audit

The kickoff meeting has been done. The work is about to start and is expected
to be performed during September,

## Blog posts

- [The Travis separation a year later](https://daniel.haxx.se/blog/2022/08/27/the-travis-separation-a-year-later/)
- [curl 7.85.0 for you](https://daniel.haxx.se/blog/2022/08/31/curl-7-85-0-for-you/)
- [curl’s TLS fingerprint](https://daniel.haxx.se/blog/2022/09/02/curls-tls-fingerprint/)

## Coming up

- curl feature window reopens on Monday!
- more websockets work and polish. Initial merge soon?
- security audit work

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

[here](all.md)
