# Daniel's weekly report

# November 11, 2022

## Known bugs reduction

This is my [funded
project](https://daniel.haxx.se/blog/2022/10/19/funded-curl-improvements/),
and I have already managed to get a few items removed from the list. I have
officially started, and I can already now sense that there is going to be work
to just avoid adding new issues to the list, let alone shrinking the list as
much as I want to.

## connection filters

Stefan took a deep dive immediately when he started his h2 and h3 related curl
projects and he decided that what better way could there be than [rewriting
lots of internals](https://github.com/curl/curl/pull/9855)? His new concept of
"connection filters" lays the foundation of further changes in the protocol
implementations going forward. I might need to write up a separate blog post
soon about what exactly this is and what it means for curl internals. It is an
internal refactor only that brings no externally visible changes.

We merged his work into master just today, Friday.

## security

We had another security issue reported and we now have two of them being
worked on lined up for the next release. Both look like they are CVE material.

The final security audit report from Trail of Bits has still not been
delivered to us, but I hear it will happens soon. Once we know we have dealt
with any security-related issues mentioned in it, we will make it public.

## noproxy

The decision to not do a quick early patch release proved to be sensible as it
turned out there were more issues left to get fixed in the noproxy regression
of last week. I hope functionality is now finally restored properly.

## httpbis

The IETF 115 meeting happens in London this week and I already before decided
to only participate from remote. However, when I was about to join the first
(out of two) meeting on Monday I realized I had to pay more than 100 USD per
meeting just to attend via video. I consider that a ridiculously steep price
and as a result I decided to not attend. I will instead rely on that all major
outcomes or discussions will show up on the mailing list sooner or later.

## Mastodon

I too am of course over on [Mastodon](https://mastodon.social/@bagder) much
more now as Twitter seems to be death-spiraling into the abyss.

## Polhemspriset

I attended the Polhem Prize awards ceremony and dinner on Wednesday. I got to
use my [suit and
bow-tie](https://twitter.com/bagder/status/1590369547122798592) and had a great
evening. This year's winner is a software person: [Staffan
Gestrelius](https://www.ingenjoren.se/2022/11/09/arets-polhemspris-gar-till-grundaren-av-qliktech/)
(page in Swedish). It has now been five years since I got the award.

## webinar

My **getting started with libcurl** webinar on Thursday went well. I have done
one before on the same topic, but this was a re-edited and improved
version. We should have a YouTube version of this up soon.

## Blog posts

- [Append data to the URL query](https://daniel.haxx.se/blog/2022/11/10/append-data-to-the-url-query/)
- [curl’s new CA store cache](https://daniel.haxx.se/blog/2022/11/11/curls-new-ca-store-cache/)

## Coming up

- Reduce the number of known bugs
- Improve websockets
- Sweep away obstacles for Stefan
- Participate in a podcast

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# November 4, 2022

## HTTP Workshop

After three blog posts about it this week I don't think I can add much more
about the Workshop. This week was all about that, with us talking HTTP over
drinks until late several night. An intense massive HTTP overdose that has
really made my brain soft by the end of the week. Can recommend!

## curl feature window

While I have been neglecting several of my duties this week, I did manage to
formally open the curl "feature window". This means that we now allow the
merging changes and new feature for the pending next curl release.

A regression in curl's `NO_PROXY` handling was reason for a minor debate if we
should perhaps rather do an early patch-release instead of opening the feature
window, but ultimately we decided the bug is not *that* bad. It also gives us
plenty of time to make sure we fix it correctly.

## Blog posts

- [HTTP Workshop 2022 – day 1](https://daniel.haxx.se/blog/2022/11/02/http-workshop-2022-day-1/)
- [Workshop season 5 episode 2](https://daniel.haxx.se/blog/2022/11/03/workshop-season-5-episode-2/)
- [thehttpworkshop2022-day3.txt](https://daniel.haxx.se/blog/2022/11/03/thehttpworkshop2022-day3-txt/)

## Coming up

- The Polhem Prize awards gala dinner on Wednesday

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

[here](all.md)
