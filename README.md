# Daniel's weekly report

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
