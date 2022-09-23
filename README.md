# Daniel's weekly report

# September 23, 2022

## spellchecks

Adding a CI job that runs a spellchecker on the entire set of libcurl man
pages turned out to be a monster job, but I pulled it through and I think it
turned out pretty good. And I did several hundred documentation fixes in the
same pull request.

It also made me do some additonal follow-up improvements of other scripts that
verify the documentation. All in an effort to make typos and mistakes less
frequent.

## API discussions

It's been one of those weeks when several API design discussions have popped
up. One is around how to manage name resolving and doing graceful fallback
down to IPv4-only when IPv6 doesn't work properly, one is around
`curl_multi_poll()` and what to do with negative timeout values and the third
that was brought up is how to improve the WebSocket API to work with (much)
larger frames than it currently does as I have been told they are quite common
in practise so my "shortcut" of only supporting smaller ones is going to put
too many hurdles in the way for real adoption.

These issues are being discussed and some of them might leed to tweaks going
forward. Designing (good) APIs is really hard.

## C99

curl is still written using C89. We have discussed maybe add a future
requirement of having a 64 bit data type (`long long`) which virtually every
compiler and system has since a long time back - and was made a standard in C
in C99. Maybe a good time to do this requrement bump would be when curl turns
25, this coming spring.

That thought subsequently brought up the discussion if we should perhaps
consider doing a jump up to **C99** as the new compliance level for curl code
while we are at it.

Would then then accept everything C99 allows or would we want to treat gently
and slowly accepting more? Is it even a good idea and does it really bring
much features we *need*? Will it cut off compatibility with some ancient
systems that a few people still build curl on?

The jury is still out on C99, but I personally think that the 64 bit data type
requirement feels like something I want: I believe the code will be easier to
manage if we can assume that the large data type is always larger than 32
bits. I doubt we can find many users still stuck on systems that do not have
64 bit types - who also need to build the latest curl.

Tell me your thoughts on this!

## funding

The idea is now to have the contracts finalized and signed mid-October. We are
going to sub-contract someone else than me as well to do work on curl using
this funding and I am super-thrilled over this opportunity and I can't wait
until I can tell you all about it!

## swag

While I am still waiting for my curl up swag to arrive, I got a huge box of
brand new swag from GitHub that included a led-octocat think that can light up
and flash in colours and patterns and more. Perks from being [a github
start](https://stars.github.com/profiles/bagder/).

## cheat sheet

Something triggered me to check out the good old curl HTTP cheat sheet, so I
created a minor update with curl colors and some minor text fixes:

[<img src="https://pbs.twimg.com/media/Fc_w1quWAAM4VUp?format=jpg&name=large" width=500>](https://curl.github.io/curl-cheat-sheet/http-sheet.html)

I still want to make a tshirt with this printed up-side-down on the front, so
that you can look down on your shirt for the hints...

## whitespace

When [RFC 9113](https://www.rfc-editor.org/rfc/rfc9113.html), the updated
HTTP/2 specification, was published in June 2022, it included new very
specific language on how to treat HTTP header fields:

    A field value MUST NOT start or end with an ASCII whitespace character
    (ASCII SP or HTAB, 0x20 or 0x09).

This language was turned into more strict checks in the very popular and
widely used [nghttp2 library](https://github.com/nghttp2/nghttp2), first
released to the public in its version 1.49.0 on August 22, 2022.

It can be noted that other widely used HTTP/2 clients, like the popular major
browsers for example, do not care about this rule violation in spite of what
the RFC says.

It did not take long until curl and libcurl users reported the first problems:
sites and services stopped working. It turns out there are quite a lot of
HTTP/2 servers out there that send trailing whitespace in their header fields
and nghttp2 returned error on that and refused to cooperate.

One of the offenders is the perhaps not too unknown service called
[WordPress](https://wordpress.com/), which then by extension made that a few
super popular RSS feeds also did not work. Like the one of [Bruce
Schneier](https://www.schneier.com/) etc.

After some frustrated ventilation on Twitter and some extremely helpful
individuals who passed on the message appropriately, [Wordpress fixed their
issue](https://twitter.com/wordpressdotcom/status/1572587600652955649).

On that same day (September 21), nghttp2 released an update. [Version
1.50.0](https://github.com/nghttp2/nghttp2/releases/tag/v1.50.0) comes with a
new option to disable the strict header check, and curl will use this option
if available. curl has however not yet done a release with that additional
logic, so even if nghttp2 now can disable the check, no released curl version
does that yet. The coming curl release is planned to be **7.86.0** and is
scheduled to ship on **October 26**.

## Vulnerability

We have received a security report about an existing vulnerability that we
have confirmed. Probably at severity **medium**. Yet another one of those
problems that have been around in the code for decades. I believe this might
be at least close to twenty years old.

## Audit

The curl security audit is continuing and we have regular meetings with status
and back-and-forth discussions and comments. They have not yet found anything
alarming but I suspect it is just a matter of time. After all, they spend
several hundreds of man hours starring and digging deep into these details so
I expect there to be stuff. Hopefully not earth-shattering though.

## Blog posts

- [Taking curl documentation quality up one more notch](https://daniel.haxx.se/blog/2022/09/22/taking-curl-documentation-quality-up-one-more-notch/)

## Coming up

- Masssaging the WebSocket API to work with large frames
- curl feature freeze on Wednesday


## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# September 16, 2022

## curl up

The zoom session went on for a little over eight hours straight, during which
we crammed in **ten** presentations on curl and related technologies.

I always love curl up - hanging out and talking curl internals, details,
specifics, bugs and dreams with a bunch of friends. It is the best event of
the year, no doubt.

Most of the talks and slides are already provided on the [agenda
page](https://github.com/curl/curl-up/wiki/2022)

Exhausting.

## printers

It's funny how libcurl is big in printers and I had a meeting with a new
customer (who shall remain unnamed) and I could help them with a range of
direct and specific advice on how to optimize their libcurl use to address
their problems and improve their performance. A very productive 30 minutes I
would say.

## audit

The curl security audit work is ongoing. We have regular meetings with Trail
of Bits for status updates and providing feedback and insights.

## funding

I now have a more detailed project description with times and costs and
everything for the three curl projects I hope to get funded. We are on track
and I expect that we can get everything agreed to and signed not too far into
the future - then I will of course let you know more details. I am so looking
forward to this!

## HTTP/3 Explained

I started writing my book *HTTP/3 explained* in February 2018 and it has been
mostly complete and done for a long time now. This week however the awesome
Marcos Medrano appeared from the shadows and brought us the brand new [Español
version](https://http3-explained.haxx.se/es)!

## Blog posts

- [convert a curl cmdline to libcurl source code](https://daniel.haxx.se/blog/2022/09/12/convert-a-curl-cmdline-to-libcurl-source-code/)

## Coming up

- more funding back-and-forth
- audit meetings
- continue on the WebSocket journey

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

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
