# Daniel's weekly report

# March 11, 2022

## Happened this week

### Vacation

I didn't do any weekly report last week because I was on vacation. I went up
north a bit in Sweden (~500km from my house) and enjoyed downhill skiing with
the family for a few days. Snow, sun and lots of time outdoors. Good times.

### Release

Due to the above mentioned ski-trip, I delayed the 7.82.0 release three days
and instead did it when I got back home. A curl release on a Saturday probably
hasn't happen in over decade or so.

We have had a few regressions reported already, but none of them have been
deemed important enough to warrant a panic follow-up patch release. On March
10 we opened the feature window and we have already merged news that will make
the next version to become **7.83.0**. I intend to do separate blog posts for
each new "thing" introduced...

### BearSSL

I brought up [the question](https://curl.se/mail/lib-2022-03/0019.html) if
BearSSL is still a library to recommend since they haven't had a commit in over
a year and is still lacking major features such as TLS 1.3.

I didn't get a whole lot of feedback, although [the author seems to think it
is fine](https://twitter.com/FiloSottile/status/1501583574675435520). I'm not
convinced, but I might leave it for now and give it another deeper look in six
months or so.

### Two-letter options

After another Twitter discussion I brought a crazy idea of how [curl could
introduce two-letter options](https://curl.se/mail/archive-2022-03/0033.html)
to the curl-users mailing list. Consider this mostly food for thoughts and a
way to bounce around some ideas on the topic. I don't think anyone thinks we
should run ahead and implement it exactly as stated there.

### Server hiccup

Our main server which runs the curl web site, mailing lists, DNS server and a
lot of other things ran into some minor problems this week (Tuesday around
15:30 UTC) which a few people noticed when some web pages started to not show
correctly on curl.se and daniel.haxx.se. The problems were mostly hidden from
the world thanks to the sites being fronted by Fastly, and after a quick
"rescue operation" from Haxx colleagues and myself, we had it up again in no
time.

### curl-minimal

Over on lwn.net, [an article](https://lwn.net/Articles/887313/) brought my
attention (still paywalled at the time of this writing) to a Fedora discussion
where they are consider shipping a stripped down "curl-minimal" package by
default, to reduce the "security surface". There are some interesting comments
and details in that discussion.

I'll keep my opinions about the main topic to myself until asked.

### curl up 2022

I started the discussion about what and [how to make curl up 2022
happen](https://curl.se/mail/meet-2022-03/0000.html).

## Blog posts

- [curl 7.82.0 Impartial Content](https://daniel.haxx.se/blog/2022/03/05/curl-7-82-0-impartial-content/)
- [Deprecating things in curl](https://daniel.haxx.se/blog/2022/03/10/deprecating-things-in-curl/)
- [remove leftovers on curl error](https://daniel.haxx.se/blog/2022/03/11/remove-leftovers-on-curl-error/)

## Coming up

- get started on implementing headers API v2 proposal
- work with PR authors and merge some pending ones

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# Older weekly reports

- [February 2022](February-2022.md)
- [January 2022](January-2022.md)
- [December 2021](December-2021.md)
- [November 2021](November-2021.md)
- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
