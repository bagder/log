# Daniel's weekly report

[Subscribe](https://lists.haxx.se/listinfo/daniel) to this as email.

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
