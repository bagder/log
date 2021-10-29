# Daniel's weekly report

# October 29, 2021

## Happened this week

- Worked more on enabling tests for hyper builds. I did a [live-coding session
  on Twitch](https://www.twitch.tv/curlhacker) (video
  [here](https://youtu.be/4arsI2VBLBo)) with a lot of work on fixing tests,
  which turned out fairly productive (the entertaining value however I'm less
  sure of =)). I'm now at **34** disabled tests remaining to fix. It is still
  too many for me to make any predictions about when I will reach zero, as it
  also depends on what other work that will fall into my lap.

- I released [c-ares](https://c-ares.org) 1.18.0 only to a few days later
  release a follow-up 1.18.1 due to a (silly) regression. I'm a c-ares
  maintainer but honestly, I don't do much in the project other than pressing
  the right key sequences when a release needs to happen. **Brad House** is the
  real hero behind most of the recent c-ares action.

- I learned that "composer 2.0", which is the current incarnation of the PHP
  package manager, is a heavy user of curl. Jordi Boggiano
  [said](https://twitter.com/seldaek/status/1452630210650726405) **98%** of
  its installs use "ext-curl", the PHP binding for curl.

- I met with "a huge biotech company" and discussed providing and supporting
  [tiny-curl](https://curl.se/tiny) on the [INTEGRITY
  RTOS](https://en.wikipedia.org/wiki/Integrity_(operating_system)) (and some
  more details). It seems like a perfect match to me and I have good feeling
  about this project.

- I published my [GitHub wish-list](https://bagder.github.io/github-feedback/),
  which is just my long-standing list of ideas I would like GitHub to address
  better.

- I (jokingly, I promise!) asked the cast of the Swedish TV series
  [hackad](https://daniel.haxx.se/blog/2021/10/19/hackad-curl-use-on-tv/) if
  they're selling sticker-space on their laptops for a possible future second
  season of the show, which ultimately had me mailing them all a set of curl
  stickers each. After all, several of their sticker-packed laptops were
  visible multiple times in the series. Now I really want there to be a second
  season and that the team actually puts curl stickers on their machines and
  then that those eventually appear on TV. Playing the long game here! :-)

- Open Source newbie ZZZZ YYYYYYY emailed me, asking about advice and
  experiences on how to think and act when running a project and since he
  reached me at a particularly good moment we had a meeting Thursday. I'm not a
  general know-it-all person on open source, but I can certainly share what I
  have learned of what has worked for me in the projects I've worked in, in
  the hopes that maybe it can work elsewhere as well.

- I managed to get myself mentioned *twice* in the most recent edition of the
  [Bulletproof TLS
  Newsletter](https://www.feistyduck.com/bulletproof-tls-newsletter/issue_82_expiration_of_dst_root_ca-causes_problems_with_lets_encrypt_certificates). Both
  for the [post-quantum
  curl](https://daniel.haxx.se/blog/2021/10/04/post-quantum-curl/) work and
  for my update on [the sad OpenSSL QUIC API
  situation](https://daniel.haxx.se/blog/2021/10/25/the-quic-api-openssl-will-not-provide/).

- We got a fun "curl sighting" in the wild: [the BMW R 1250 GS
  Adventure](https://www.bmw-motorrad.co.uk/en/models/adventure/r1250gsadventure.html)
  motorbike is obviously using it. The image of the curl license shown on the
  bike's display is now up on [the screenshot collection
  page](https://daniel.haxx.se/blog/2016/10/03/screenshotted-curl-credits/) of
  mine.

## Blog posts

- [The QUIC API OpenSSL will not provide](https://daniel.haxx.se/blog/2021/10/25/the-quic-api-openssl-will-not-provide/)
- [a GitHub wish list](https://daniel.haxx.se/blog/2021/10/26/a-github-wishlist/)

## Coming up

- Next week we've switched off Daylight Saving in Europe but not in the US and
  this makes it the "crazy time zone week". The US switches a week later.
- More hyper fixes
- a libcurl presentation for wolfSSL engineers on Thursday
- On Nov 4 we've had the curl website on [curl.se](https://curl.se/) for a
  whole year

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# October 22, 2021

## Happened this week

- The trial I've mentioned before in which I was going to be an expert witness
  was settled, so I didn't get to do anything in court...

- The Swedish TV-show 'Hackad' aired and I got help by friends to identify a
  few scenes that use curl. So I blogged about it.

- I was a guest on the [Inside Security](https://youtu.be/06Xfa2AvQrw)
  podcast, and talked about curl... This made it my 25th ever [podcast episode
  participation](https://daniel.haxx.se/podcasts.html)!

- The **getting started with libcurl** webinar happened. I'll post a YouTube
  link here and on twitter once it becomes available.

- I've returned to working on [the hyper
  backend](https://github.com/curl/curl/wiki/Hyper) in curl this
  week. Basically grabbing one disabled test case at a time. The goal is to
  have no tests "batch disabled" because of hyper. They all need to be
  investigated and either: A) disabled in the test because the test verifies
  something hyper doesn't support (should not be very common) or B) the test
  should be made to work when built with hyper. In the (B) cases, it might
  mean fixing the test or fixing the curl code, depending on the
  circumstances.

- We officially dropped out from `hacktoberfest` this week. Mostly because
  their setup and new requirements annoys me: previously we've just had to add
  the right label to the GitHub repo and once someone's PR was merged, they
  could apply for a tshirt etc. This year however, they have changed the rules
  so they no longer accept the way we merge pull-requests in the project as
  the "legitimate way" for users to claim they had it merged. We now need to
  add a special tag on every PR that is deemed fine for hacktoberfest. Since
  we don't know which PRs that would be considered, we would basically have to
  add it to every PRs or the PR author would have to ask for it (which might
  not be obvious to that person).

- I received a [GitHub star
  key cap](https://twitter.com/bagder/status/1450073498349707268).

## Blog posts

- [Hackad: curl use on TV](https://daniel.haxx.se/blog/2021/10/19/hackad-curl-use-on-tv/)
- [The most used software components in the world](https://daniel.haxx.se/blog/2021/10/21/the-most-used-software-components-in-the-world/)

## Coming up

- More hyper fixes. I can sense that there's light somewhere at the end of
  this very long tunnel...

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# October 15, 2021

## Happened this week

- I joined [Eddie Jaoude's
  live-stream](https://www.youtube.com/watch?v=X5SGO8cUG8o) on Monday and we
  talked curl, working on open source and exactly how widely used curl is for
  over an hour. Lots of fun.

- I presented [curl is
  everywhere](https://daniel.haxx.se/media/netnod-curl-is-everywhere-2021.pdf)
  at the Netnod Tech meeting. My first presentation done in person since
  February 2020! I felt a little "rusty" but I think it was appreciated and
  got some good questions in the end.

- I reviewed a coming security paper on problems and insecurities with
  different URL parsers, and since the authors of this report found a related
  curl bug I fixed how curl [didn't do percent decoding of host
  names](https://github.com/curl/curl/issues/7830). Not at all as
  straight-forward as it sounds...

- I sent off a contract development proposal for a feature I know lots of
  people would like.

- I worked on some tiny-curl issues I shipped in the recent release, mostly as
  a result of the internal changes of select-handling between the two most
  recent tiny-curl releases. There will be a tiny-curl patch release soon.

## Blog posts

- [Coming webinar: getting started with libcurl](https://daniel.haxx.se/blog/2021/10/12/coming-webinar-getting-started-with-libcurl/)
- [curl installations per capita](https://daniel.haxx.se/blog/2021/10/15/curl-installations-per-capita/)

## Coming up

- I'll serve as an "expert witness" on Wednesday in a trial involving
  web-scraping

- I'm doing a podcast appearance on Tuesday

- The **getting started with libcurl** webinar happens on Thursday

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# October 8, 2021

## Happened this week

- Nova 2021 was an online GitHub star conference that ran Monday/Tuesday this
  week. I browsed it casually since it was awkward time zone wise and I feel
  that a lot of what GitHub works on these days are not things that concern me
  much.

- I did a curl talk Wednesday for a Swiss company. This, my 91st talk in front
  of an audience since 2015 had large overlaps in topic and slides with my
  92nd talk I will do next week at Netnod.

- I made a [roffit](https://github.com/bagder/roffit) 0.13 release, which is
  the first "official" roffit release I've tagged and marked as a release on
  GitHub. Figured it was about time since we've now used roffit on the curl
  site to render man pages into HTML for fourteen years or so!

- I worked on the Netnod presentation and sent off [the
  slides](https://daniel.haxx.se/media/netnod-curl-is-everywhere-2021.pdf).
  They want them ahead of time to put them on a presentation computer. Makes
  me appreciate the LibreOffice macro I use that expands animations into
  multiple PDF pages so that I can provide a standard PDF that still has the
  animations (lines appearing line by line etc) that I like to
  use. LibreOffice's ability to export to the keynote or PowerPoint formats is
  way too bad.

- I worked on content for my webinar on October 21, **getting started with
  libcurl**. I want the presentation to run no longer than maybe 30 minutes
  and it takes some trimming and thinking to make sure I get as good content
  as possible in that limited period.

- I was contacted by a security research team who is currently working on a
  security paper on URL parsers and problems with them and I had the pleasure
  of reviewing it.

- Made [a new graph](https://twitter.com/bagder/status/1446029094236348416)
  for the [curl dashboard](https://curl.se/dashboard.html). It measures the
  life-time of all issues that are fixed/closed with a git commit
  message. Turns out the 12 month median time is now less than 20 hours.

- I finally pressed the magic keys in the right order on my router and now I
  have working IPv6 connectivity in my household.

## Blog posts

 - [Post-Quantum curl](https://daniel.haxx.se/blog/2021/10/04/post-quantum-curl/)
 - [One new contributor every 3.4 days](https://daniel.haxx.se/blog/2021/10/04/one-new-contributor-every-3-4-days/)

## Coming up

- I'll join Eddie Jaoude's live-stream on Monday! Follow my [twitter
  stream](https://twitter.com/bagder) for details.

- I'm doing a curl talk at Netnod tech meeting on Wednesday.

- Also Wednesday: we enter **feature freeze** in the curl project. This means
  that we will not merge any more features and only work on bug-fixes for the
  following four weeks, with the goal of shipping curl 7.80.0 on November 10.

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# October 1, 2021

## Happened this week

 - Opened the [feature window in
   curl](https://curl.se/dev/feature-window.html) this Monday and we've merged
   several changes already - with more probably coming.

 - Rabbit hole #1 of the week was when I found a single NTLM curl test case
   that started to consistently fail on macOS with OpenSSL 3.0.0. After a few
   hours of narrowing down, I learned that the OpenSSL function `DES_set_key()`
   (sometimes?) refuses to work if a "bad" key is used, which in NTLM is easy
   to trigger if a very short password is used as then one of the keys it uses
   will be all zeroes. We had used this DES function for NTLM for over
   **seventeen** years so saying this was surprising is not overstating it. I
   don't know why this only triggered on macOS but the solution was
   nonetheless to switch to the function without the "safe" check:
   `DES_set_key_unchecked()` - and peace was again restored...

 - The IETF HTTP Working Group had two separate two-hour interim meetings, on
   Tuesday and Thursday which both started 23:00 my time and made me a bit
   unfocused during them. They of course covered mostly interesting topics
   that to a large degree probably will end up addressed in curl sooner or
   later...

 - Rabbit hole #2 of the week: Ryan Sleevi posted curl issue
   [Inconsistent/Incompatible handling of filename escaping in
   multipart/form-data compared to RFC 7578 and
   browsers](https://github.com/curl/curl/issues/7789) which details how when
   doing multipart formposts (like with curl's `-F`), the way to encode
   special characters in file and field names have changed in recent specs and
   Firefox and Chrome both now encode them differently (now using
   percent-encoding) than way back (for at least Firefox this is a recent
   change, that happened somewhere between version 88 and 92). curl still
   encodes the names using "the old" way (using a backslash method). The
   correct course of action for this is not easy to tell as of this moment, as
   server-side receivers certainly will now have to deal with both encoding
   methods for the foreseeable future. My gut feeling says that when all the
   browsers have switched to percent-encoding, it is only a matter of time
   until using the older encoding will cause problems...

 - The certificate for `https://libssh2.org` (without `www.`) expired. As I'm
   not the owner of the DNS for the domain there was a gap until the site and
   cert were functional again on that name.

 - On the topic of certificates I guess nobody missed the expiry of `DST Root
   CA X3` on September 30. I fixed the [conversion
   script](https://github.com/curl/curl/blob/master/lib/mk-ca-bundle.pl) to
   make sure the curl webpage that [provides the Mozilla CA cert
   bundle](https://curl.se/docs/caextract.html) now leaves it out as well.

 - I made a [tiny-curl 7.79.1](https://curl.se/tiny/) release.

 - I vented on twitter about the strange starting years mentioned in [the curl
   wikipedia page](https://en.wikipedia.org/wiki/CURL), and voila, now they
   have been corrected...

 - Several good meetings this week with old customers, new customers and
   potential new customers!

 - I ran [a quick poll on
   twitter](https://twitter.com/bagder/status/1443465922686201857) and got it
   confirmed that there is an interest in a "getting started with libcurl"
   presentation/webinar. Mark October 21 in your calendars for this! I'll do a
   separate blog post about it soon.

## Blog posts

 - [curl’s first twenty years on the mac](https://daniel.haxx.se/blog/2021/09/25/curls-first-twenty-years-on-the-mac/)
 - [Common mistakes when using libcurl](https://daniel.haxx.se/blog/2021/09/27/common-mistakes-when-using-libcurl/)
 - [My weekly reports](https://daniel.haxx.se/blog/2021/09/30/my-weekly-reports/)

## Coming up

 - Doing a few private commercial releases for customers
 - A private presentation for company SSSSSSS on Wednesday
 - Write up a plan for feature NNNNNNN and see if we and company VVVVVVVVV
   can agree on how to fund this!
 - Start finalizing my presentation for October 13

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older reports

- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
