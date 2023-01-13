# Daniel's weekly report

[Subscribe](https://lists.haxx.se/listinfo/daniel) to this as email.

# January 13, 2023

## weekly

This report, my weekly report, is now possible to subscribe to as a weekly
email. Subscribe here: https://lists.haxx.se/listinfo/daniel

I was already emailing this to some receivers and I decided I might just as
well open this up for anyone who wants to. I have not fully decided yet, but I
might switch over to do email only soon. Let me know if this would be a
problem for you.

The emails are and will be archived here: https://lists.haxx.se/pipermail/daniel/

I might need to experiment a little with the exact formatting of the report
as maybe markdown is not ideal for emails.

## httpd tests

The initial PR with Stefan Eissing's work on yet another test suite for curl
was merged. This new test suite is designed and intended to much better allow
h2 and h3 testing with potentially large amount of parallel transfers.
Something the existing test suite is really bad at.

This new test suite is still in its early days, but should help us not only
test and verify h3 going forward on its way to become non-experimental but
will also help us test and polish h2 functionality. A proper test suite make
things so much better!

## vacation

I will be away from computers and spend the next two weeks mostly offline
without much ability to watch the project or even read email. If anything
appears in the project in the meantime that needs my help or input it will
just have to wait until I get back.

I have not had this long planned total offline vacation from curl in many
years. It's also a little bit like a test how well things can run in my
absence. According to stats, I merged 81% of all commits during the last
twelve months and authored 56% of them.

If you need me for anything in my absence, please consider waiting until I get
back before you ask, email or file that issue to make the pile of backed up
stuff for when I get back a little less intimidating.

I'll be back in time to work on the 7.88.0 release.

## feature freeze

The curl feature freeze was originally meant to happen on January 18th but due
to my vacation I decided to call it early and close the proverbial gates
already this weekend before I leave for my vacation.

This is going to become an *extended* feature freeze because after the next
release (7.88.0 on February 15th) there will not be another feature window but
only bugfixes again until March 20 when we intend to ship **curl 8.0.0.**...

## HTTP/3 steps

On our path towards removing the **experimental** tag from the curl HTTP/3
support, we decided to tweak the options for how users ask for it. The
`--http3` option will be transitioned over to asking for HTTP/3 but also do a
fallback to an earlier HTTP version in case HTTP/3 doesn't work. We believe
this is what most users will want, since so many servers don't do HTTP/3 yet
and also because quite a few organizations and companies block UDP
traffic. curl will do h3/h2 attempts happy eyeballs-style: start an h3 attempt
at the same time as the h2/h1 attempt, with the latter only slightly delayed
to give h3 a minor preference. The first one that then succeeds to connect
wins and will be used for the transfer.

A new `--http3-only` option is also introduced. Of course both of these
command line options have their corresponding values for the libcurl
`CURLOPT_HTTP_VERSION` option.

To better allow for even more HTTP versions in the future (yes I believe such
will come, eventually), I will probably change the command line tool options
for this before we remove the experimental label. A `--http-versions` or
similar option could maybe be a single replacement for several of the old HTTP
version selector options. I'll get to work on that when I get back from
vacation.

## AAAA

Several friends have pointed out to me that many websites that I host (like
`lists.haxx.se` and `libssh2.org`) don't have working IPv6 connectivity while
they are announcing AAAA entries in DNS. And yeah, I know about this annoyance
and this week I invested some time to solve it but again I had to admit defeat
for now.

We run a setup with nginx as reverse proxy and each separate domain/website in
its own docker container, which when things work is a really convenient and
neat way to compartmentalize everything so that each website is separately
setup, configured and truly can't interfere with the others. But the downside
is that the IPv6 and networking setup is a little complicated and I haven't
yet worked out what to do to get it working. I will work on it more going
forward.

For the biggest websites I run (`curl.se` and `daniel.haxx.se`) this is not a
problem because they are fronted to the world by Fastly and they offer proper
IPv6 functionality.

## Crashes

We have had a few crashes reported recently that revealed the boring truth
that they happen because (some) applications subtly *abuse* the libcurl API
and call `curl_global_cleanup()` while there are still some transfer in
progress. This is clearly documented as not to be done. However, quite clearly
this has been possible without any major drawback for a long time so now when
crashes suddenly occur after an upgrade to the latest curl release, users
unsurprisingly blame libcurl for this since "it worked fine with older
versions".

We ended up changing the code around a bit in an attempt to again make
`curl_global_cleanup()` a little less likely to go belly-up in these
situations. Not the least because the crash that happens is not very easily
detected to happen because of this mistake.

## podcast

I am starting an English-speaking podcast together with some fellow Swedish
open source peeps. Names and details will follow later.

## Blog posts

 - Copyright without years: https://daniel.haxx.se/blog/2023/01/08/copyright-without-years/
 - My weekly report on email: https://daniel.haxx.se/blog/2023/01/10/my-weekly-report-on-email/
 - Selecting HTTP version (three): https://daniel.haxx.se/blog/2023/01/12/selecting-http-version-three/

## Coming up

- Two weeks of vacation (with no weekly reports)

# January 8, 2023

## Copyrights

Instead of bumping curl copyright year ranges to show 2023, we decided to
remove the years completely! This means that we have now finally made the last
updates of copyright years in curl source headers and feels like a relief.

## GSKit

A discussion fired up in the curl camp about the future and handling of the
TLS backend called GSKit, primarily used on the systems formerly known as
AS/400 (nowadays called IBM i). We don't have any CI builds for this and when
we break the code it can take a long time until someone notices. Not at good
situation for code that handles security related things for curl.

gskit is now mentioned as deprecated and is subject for removal, but there are
noises being made and there is hope that it will be rescued and brought up to
shape so that we can avoid ripping it out.

## noproxy

The concept of specifying `NO_PROXY` to exclude certain hosts from using a
proxy is not defined by any standard and spec. (Stan Hu wrote [this nice
summary of the
situation](https://about.gitlab.com/blog/2021/01/27/we-need-to-talk-no-proxy/)
two years ago.)

It was pointed out that curl supports a list of **space**-separated patterns
in addition to the more common **comma**-separated list. Allowing just space
for this is more of an accident and has now been marked as deprecated and the
support of those will be removed... in 18 months. Most implementations agree
that comma is the correct separator.

## HTTP

Stefan's HTTP work has continued and we have worked a bit on the aftermath of
the most recent refactor as a few regression turned up. There is a little more
work needed to get the msh3 HTTP/3 backend back to functionality, but we are on
it.

Stefan is working on a huge new test suite for HTTP/2 and HTTP/3 which is
going to help us make sure we can remove the experimental tag from HTTP/3
support later this spring.

## HTTP/3

As a step towards enabling HTTP/3 support for everyone we have also started to
discuss exactly how users would like to ask for HTTP/3 and how to do fallback
properly in case HTTP/3 doesn't work - as we expect HTTP/3 to not be too
widely supported just yet plus the fact that lots of companies and
organizations actively block UDP and therefore prevents QUIC from working.

We also want to be able to transition into having such options enabled by
default at some future point when HTTP/3 is prevalent to motivate it.

Right now, we aim at doing h3/h2 connections a little happy eyeballs style:
start the h3 attempt a short moment before we start a parallel h2 attempt, and
then we go with the connection that succeeds first.

## Blog posts

 - nothing this week

## Coming up

- 10 days until feature freeze
- my last week before a two week vacation
- wolfSSL team meeting

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

[here](all.md)
