# Daniel's weekly report

# December 30, 2022

## Happy New year

My last weekly report for the year. Happy New Year everyone!

## Hardware

While I am awaiting the last component for my new development PC to arrive at
my house, I received a mac mini m1 donated to me and I set it up yesterday and
did some initial curl builds to try it out. This should allow me to better
work on some m1 related curl issues we have seen mentioned recently.

Of course it also reminded me how annoying macOS is and how glad I am I can
stick to my trusted Linux most days.

## HTTP refactor

Stefan Eissing has a huge PR up for merge that is rearranging a lot of HTTP
internals to prepare for more future protocol fun, and I am working with
reviewing that work and bouncing ideas on how things could or should be done.

We had a productive design meeting this week with msh3-Nick and we agreed on a
way forward for how to integrate ms3h into the mix as well so that we can move
forward with all three supported QUIC/h3 backends.

This week we created a list of a few requirements we have for HTTP/3 support
in curl to work before we can remove the 'experimental' label from it.

Stefan also works on a new test suite for curl, very creatively called "httpd
tests", which are going to add a new set of HTTP tests we previously have been
lacking. Primarily for HTTP/2 and HTTP/3 testing, including multiplexing with
potentially a large number of streams both concurrently and serially. HTTP
tests at a layer we have previously have not been able to test properly before
with the existing curl test suite.

This new test suite will be used to verify and fix pending HTTP/3 issues, with
the goal of enabling HTTP/3 "for real" in all builds at some point in early
2023.

One of the requirements for "HTTP/3 for real" in curl is that we have a decent
way for users to ask for HTTP/3 with graceful downgrade to earlier HTTP
versions if h3 does not actually work.

## Blog posts

 - [At 17000 curl commits](https://daniel.haxx.se/blog/2022/12/27/at-17000-curl-commits/)
 - [curl -w certs](https://daniel.haxx.se/blog/2022/12/28/curl-w-certs/)
 - [An m1 for curl](https://daniel.haxx.se/blog/2022/12/30/an-m1-for-curl/)

## Coming up

 - 2023
 - Merge Stefan's huge PR
 - Work on fallout from the new test suite?

# December 23, 2022

## Merry Christmas

This is the Christmas episode of Daniel's weekly, and I will probably be
slower than usual next week. I do not do any yearly summaries for curl around
new year as I rather sum them up later in the spring around our curl up
event. You can of course view lots of activity graphs yourself on [the curl
dashboard](https://curl.se/dashboard.html).

## Release

I pushed out the curl 7.87.0 release on December 21. We have received a few
early bug reports, some of them identifying regressions, but so far they have
been innocuous enough to not force us into a patch release. The final decision
on re-opening the feature window will be done late Sunday my time.

The next curl release, most likely to called 7.88.0, is also planned to become
the last ever curl version 7 release. Release date February 15, 2023.

The plan is then to ship curl 8.0.0 on March 20, 2023. Between 7.88.0 and
8.0.0 there will not be any open feature window.

## Audit

The security audit report finally went public this week, and while there was
no alarming issues or news in there, I still feel happy about it and now the
world can check it out and maybe get seem help on how to assess our little
project.

## IDN article

I translated my "IDN is crazy" blog post into Swedish and polished it somewhat
and with some help it might soon get included in a local tech related
magazine. Possibly even in a print version I suspect. I will of course brag
about it later when/if it actually happens.

## Security

Did I mention that security is hard? I had basically just sent off the release
announcements for 7.87.0 and was still sitting with my feet up when new
security vulnerability reports landed in our knees and now we already have two
new security problems confirmed. They are both set to severity levels lower
than high so they are targeted for getting fixed and announced with the next
planned release.

## Blog posts

 - [curl sighting: Tschugger](https://daniel.haxx.se/blog/2022/12/19/curl-sighting-tschugger/)
 - [curl 7.87.0](https://daniel.haxx.se/blog/2022/12/21/curl-7-87-0/)
 - [The 2022 curl security audit](https://daniel.haxx.se/blog/2022/12/21/the-2022-curl-security-audit/)
 - [The curl fragment trick](https://daniel.haxx.se/blog/2022/12/23/the-curl-fragment-trick/)

## Coming up

 - Christmas
 - end of year slow-down
 - opening the curl feature window?

# December 16, 2022

## Release prep

I have worked on the curl release blog post this week to highlight the most
significant activities we did since the previous release, as usual. The slides
for the release video presentation are also nearly done. Things are lining up
nicely. Two new CVEs will be published in association with the release,
severity medium and low.

## Security audit

The audit report is finally going to get published next week, on the same day
of the pending curl release, only later in the day so that the Americans that
are involved get time to wake up first. Stay tuned for blog posts and
announcements on Wednesday.

## IDN

I toyed a little with IDN this week, one result being the blog post about how
crazy this system is. It also made me realize that we probably want to allow
the libcurl URL API to the punycode version of a given URL or host name using
an IDN hostname so that users at least can attempt to get a canonical version
of a given URL. I am going to work on adding this feature for a future
release.

## Mastodon

I am decreasing my activity on [Twitter](https://twitter.com/bagder) and
increasing in on [Mastodon](https://mastodon.social/@bagder). Follow me over
to keep the noise about curl, networking, URLs and more uninterrupted.

## Blog posts

- [curl sighting: Silk Road](https://daniel.haxx.se/blog/2022/12/10/curl-sighting-silk-road/)
- [IDN is crazy](https://daniel.haxx.se/blog/2022/12/14/idn-is-crazy/)

## Coming up

- curl 7.87.0 release
- security audit report gets published

# December 9, 2022

## base64

I accidentally fell over and drastically improved base64 encoder and decoder
performance. It was of course properly satisfying, even if it mostly
identified existing slow code rather than me doing something magic. See my
blog post for all the details.

## dev machine

As I revealed numbers from my base64 endeavors mentioned above, it become
evident that my current dev machine is not very fast. I suspect it being ten
years old kind of gives that away but still. I got some help and I have
ordered a new one as a set of components. I will of course get back with all
the details and a full report about how much faster I can build curl once the
upgrade has been performed.

## FOSDEM

FOSDEM announced the [accepted
stands](https://fosdem.org/2023/news/2022-12-08-accepted-stands-fosdem-2023/)
for 2023, and wolfSSL is listed. I plan on making sure that there will be curl
stickers there for all those who want some and fail to catch me at the event.

## hyper

I managed to circle back to hyper issues and we have now enabled another test
case for the hyper builds. Ironically, we are now back down to 13 disabled
tests, which happened to be exactly where we were at in May as well.... Ups
and downs.

## known bugs

I've continued to clean up the list of "known bugs" and decimated the amount
further this week. Not so much by actually fixing code but more by documenting
facts and by simply closing things we haven not heard about for decades.

## websocket

I feel I have neglected this area recently and I hope to come around back to
Websocket again soon so that we can continue to polish it. I still wish we had
more interested users actually testing it out, but I will of course still go
with what we have.

## everything curl

I wrote a brand new page explaining [how we work with timeouts
internally](https://everything.curl.dev/internals/timeouts) in libcurl, for
the *internals* sections of [everything curl](https://everything.curl.dev/).

## Blog posts

 - [Faster base64 in curl](https://daniel.haxx.se/blog/2022/12/06/faster-base64-in-curl/)

## Coming up

- pre-alert the distros mailing list about two coming curl CVEs
- slowly start preparing for the curl release

# December 2, 2022

## 5-digit issue numbers

On GitHub, the curl project broke the limit and is now in the 5-digit range of
issues and pull-requests after [almost eight
years](https://daniel.haxx.se/blog/2015/03/03/curl-embracing-github-more/) of
using it as our primary "tracker".

This is of course just another number without any inherent meaning. We expect
the next 10,000 issues to go faster than the first set.

## TLS

Stefan Eissing's continued work on connection filters for curl internals made
us merge his TLS rework this week, and as a direct result of that curl now
supports HTTPS proxies with many more TLS backends than before. The notable
part of using HTTPS proxies of course being that speaking HTTPS over them
makes the transfer do double TLS.

## h3 tests

During our recent refactor work of connection and HTTP internals we managed to
accidentally break HTTP/3 support several times, because we did not have any
HTTP/3 tests running in our CI. We only verified HTTP/3 *builds* which
obviously was not good enough. This was not any surprise really, but Stefan
did good work in that area as well and now we at least have an initial test
(and framework) that verifies very basic working HTTP/3 in curl. I expect us
to extend this more going forward.

## `%{certs}`

Someone wanted to get the server certificate chain from an HTTP/3 server.
Typically users use the openssl tool for this, but it doesn't support
HTTP/3. Since libcurl already has this ability but it just isn't exposed to
the tool, it was easy to [created a draft
PR](https://github.com/curl/curl/pull/10019) to work out how this can be done
by curl's `-w` option in the future.

## Blog posts

No posts this week

## Coming up

- more of the same

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

[here](all.md)
