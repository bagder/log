# Daniel's weekly report

# April 1, 2022

## Happened this week

### New CVE coming

We've worked a little on a pending new CVE for curl that has been reported and
confirmed. It is a security vulnerability and we have a patch done
already. Left to do is to write up a thorough and complete advisory and soon
to apply for a CVE id for it. This is going to be first security vulnerability
in curl that is eligible for a reward via [the Internet Bug
Bounty](https://hackerone.com/ibb), which curl is a part of since last year.

We will publish the CVE details in sync with the next release, planned to
happen on April 27.

### busy-loop

An separate issue filed as a suspected security vulnerability was the MQTT
busy-loop I blogged about. It was one of those tricky problems that took me a
few days to make up my mind about before I landed on *not* a security issue.

The reporter, Jenny Heino, wrote a [blog post about the
finding](https://nyget.in/2022/03/28/my-first-fuzzy-finding-busyloop-in-curl/)
from her point of view.

### h2-bugs

You would like to believe that the HTTP/2 logic in libcurl would be fairly
stable by now, but... there are always more polish to be done. We fixed
several minor issues, in what are probably [edge
cases](https://github.com/curl/curl/issues/8626) but still.

### Generic TLS (ALPN) messaging

I did some tidying up among the TLS backends and have introduced common
strings for some ALPN related verbose messages. The point would be to
make curl output the same messages about TLS related things, independent
of which backend that is used. I started doing this for ALPN related
texts but I figured this is a good idea in general so hopefully I will
get to making more strings identical this way.

### Feature freeze

On March 30 we closed [the feature
window](https://curl.se/dev/feature-window.html) for this cycle. Now we
will only merge bug-fixes till the next release.

### Podcast

My podcast appearance on software engineering radio went up this
week. An compact hour of me talking a lot about curl, development,
releases, production, success and more.

### Everything curl

The [book](https://everything.curl.dev/) grew over 700 lines this week
and is now more than 90,000 words and 13,000 lines.

I added new pages about caches, alt-svc and the `curl_easy_option` API etc.

I've cleaned up the language use on words like runtime, wildcard, "an
HTTP" (as compared to "a HTTP") and use of uppercase URL. Consistency is
king.

## Blog posts

- [What curl expects from dependencies](https://daniel.haxx.se/blog/2022/03/28/what-curl-expects-from-dependencies/)
- [This busy-loop is not a security issue](https://daniel.haxx.se/blog/2022/03/28/this-busy-loop-is-not-a-security-issue/)
- [Talked curl on software engineering radio](https://daniel.haxx.se/blog/2022/03/31/talked-curl-on-software-engineering-radio/)

## Coming up

- curl on Win CE for customer
- customer meeting talking deep libcurl debugging in mobile phone apps

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

- [March 2022](March-2022.md)
- [February 2022](February-2022.md)
- [January 2022](January-2022.md)
- [December 2021](December-2021.md)
- [November 2021](November-2021.md)
- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
