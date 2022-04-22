# Daniel's weekly report

# April 22, 2022

## Happened this week

### Uncurled

At 15,400 words.

### Security

Oh man, last week I was still in blissful ignorance of what would come. I was
planning for a single CVE advisory and publication in association with the
pending release coming up next week on April 27.

Then Harry Sintonen "happened" as he ruthlessly reported **three** additional
problems to us, making most of my week getting spent on researching,
debugging, patching, requesting CVEs, pre-alerting and writing security
advisories. Let's hope we have stopped on four for this time.

None of these new security problems are of the soul-crushing earth-ending kind
but they are still bad enough to cause my brain to hurt. You will of course
get to read all the details on Wednesday.

### Cyber Safety Review Board

I participated in a meeting with the US [Cyber Safety Review
Board](https://www.cisa.gov/cyber-safety-review-board) (I love saying that
name) this week with two fellow Open Source maintainers from well-known
projects and talked Open Source, development, security, slow upgrade cycles
and helped explain how all this is done and works. I would like to believe
that we contributed a little to educating influential people on this topic. I
have no idea if it ultimately changes anything.

### curl up

We announced [curl up 2022](https://github.com/curl/curl-up/wiki/2022) and
that it will take place in San Francisco on June 6. This is the first curl up
in North America and it is arranged by [wolfSSL](https://www.wolfssl.com/). I
am really looking forward to this!

I rely on users and developers to tell me what you want to talk about or to
listen to, and of course that you want to help sponsor the event.

curl up 2022 is going to be a full day with curl and curl-related
presentations by yours truly and ideally a handful of knowledgeable curl
developers and curl users.

This will also be the first time since 2016 that I will travel to the US
again. If you want to meet up over a coffee or pick my brains for something
while I'm there, you know where to find me.

## Blog posts

 - [curl up 2022 San Francisco](https://daniel.haxx.se/blog/2022/04/20/curl-up-2022-san-francisco/)

## Coming up

 - the 7.83.0 release, with a release video presentation as usual
 - nail down some more curl up details and agenda items
 - curl webinar on Thursday? Not sure I will manage that...
 - a curl presentation for a well-known car company on Friday

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# April 15, 2022

## Happened this week

### Vacation

I spent 4 days of this week away from the keyboard together with my family and
it was great. Now there's a four-day weekend following (national holidays on
Friday and Monday).

### Uncurled

My Uncurled book project is now at 11,900 words as I've added more content,
but I have also thought of some more chapters to add so I imagine I will be
able to add several thousand more words given a little more time. I will use a
few more weeks on it before I announce for real and give away the URL in
public.

As a little side-effect, as I added a CI job that runs a spellchecker on the
content I also went through and added a spellcheck CI job to "everything
curl", which was quite tedious since it features soooo many words that do not
exist in the existing word lists. Still, I did it and this shall hopefully make
it easier for me to maintain better spelled books going forward.

### msh3

I merged Nick Banks' PR that brought msh3 support to curl. msh3 is another
HTTP/3 library, which then makes curl support three different ones - all still
in experimental mode.

We support many backends of protocol handlers like this to allow users to
select which ones they want curl to use. "Let a thousand flowers bloom" etc
and by allowing them to "compete" against each other we can either let them
all remain supported if that is what the community wants or if, over time, one
of them seems to become the leader or "the winner" we could maybe go with that
in a future.

We also help the ecosystem of h3 libraries and h3 implementers to test more
combinations.

## Blog posts

- [More steel](https://daniel.haxx.se/blog/2022/04/09/more-steel/)
- [msh3 as the third h3 backend](https://daniel.haxx.se/blog/2022/04/10/msh3-as-the-third-h3-backend/)

## Coming up

- inform distros@openwall about the pending CVE announcement
- meeting about about open source supply chain security Thursday with ZZZZ
- start putting together the 7.83.0 release presentation

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# April 8, 2022

## Happened this week

### Uncurled

I have had a few pending blog posts about doing Open Source in draft
state for a few years by now and this week I finally made up my mind:
instead of making these blog posts, I am going to convert them and
gather other notes, thoughts and documents of mine into *a book* about
my experiences and lessons from a life (well, three decades at least)
with Open Source. I've started the work without yet announcing where/how
the work in progress can be seen, although lots of good people of course
have found it and started to provide feedback and help me out. I am
blessed with the best friends.

I am happy with what I have managed to blurt together already the first
few days (at 8,500 words and counting), and there is still more to write
and expand on. I really need to consider how to properly put it all
together in a comprehensible way. To make the result approachable and
decently readable. But I am not in hurry.

If you have ideas of what you would like to see me cover, let me know.

I asked for [title
suggestions](https://twitter.com/bagder/status/1512082889130741774) on
Twitter and I got a flood of good suggestions back. I have decided to go
with:

**Uncurled** - everything I know and learned about running and
maintaining Open Source projects for three decades.

### Rate limit curl

I grabbed another old outstanding bullet point from the TODO document in
the curl repository and put together a new command line option proposal
for curl. Using this, tentatively called `--rate`, option you can ask
curl to [do transfers/requests no faster
than](https://github.com/curl/curl/pull/8671) N transfers per M time
units when you ask curl to do multiple transfers in a serial manner.

Very early days still for it, but I'm open for your criticism and
feedback on how it planned to work.

### Deprecate RANDOM_FILE and EGDSOCKET

In one of my passes of the curl source code, it struck me that we have
two setopt options for libcurl that are not in effective use
anymore. The `CURLOPT_RANDOM_FILE` and `CURLOPT_EGDSOCKET` options were
only supported with older OpenSSL versions that mostly are extinct now.

I'm moving forward to [deprecate
them](https://github.com/curl/curl/pull/8670) and their command line
option companions.

### Android debugging

I had a productive meeting with customer S and their somewhat strange
problems with `curl_multi_wakeup()` on Android. We have some ideas on
further debugging, logging and analyzing strategies that should help us
continue to narrow down and understand when and why the problem appears...

### WinCE 

Meanwhile, customer W had virtually no issues at all building and
running a recent libcurl version for WinCE 5.0.

### curl up

At our weekly curl meeting yesterday at [wolfSSL](https://wolfssl.com)
we decided to move forward and try to organize something curl up - like
in San Francisco. We are now investigating the venue situation. More
details to follow soon if things just line up as we hope to.

### User survey

I started to go over the questions in the annual curl user survey to
freshen them up and also edit them based on feedback we got last year -
add/remove answer alternatives, maybe remove some questions and see if
we should add something. Right now, I aim at making the survey go live
on Monday May 16th.

## Blog posts

- no posts this week

## Coming up

- I will be off next week, going somewhere a few days in search of spring

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


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
