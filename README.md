# Daniel's weekly report

# October 22, 2021

## Happened this week

- The trial I've mentioned before in which I was going to be an expert witness
  was settled, so I didn't get to do anything in court...

- The Swedish TV-show 'Hackad' aired and I got help by friends to identify a
  few scenes that use curl. So I blogged about it.

- I was a guest on the [Inside Security](https://youtu.be/06Xfa2AvQrw)
  podcast, and talked about curl... This made it my 25th ever [podcast episode
  participation](https://daniel.haxx.se/podcasts.html)!

- The **getting started with libcurl** webinar happened. I'll post a youtube
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

- I received a [github star
  keycap](https://twitter.com/bagder/status/1450073498349707268).

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

- The **gettting started with libcurl** webinar happens on Thursday

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
  me appreciate the libreoffice macro I use that expands animations into
  multiple PDF pages so that I can provide a standard PDF that still has the
  animations (lines appearing line yb line etc) that I like to
  use. libreoffice's ability to export to the keynote or powerpoint formats is
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
   change, that happened somewhere between verion 88 and 92). curl still
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


# September 24, 2021

## Happened this week

 - I did my [just curl
   it](https://www.webexpo.net/prague2021/talk/just-curl-it) presentation on
   WebExpo in Prague. Just a little over 40 minutes of me blabbing. To my
   great disappointment there was not a single question for me in the Q&A in
   the "speaker's corner" afterwards!

 - Shipped curl 7.79.1 on Wednesday with all that entails. This time no major
   regression has yet been detected so the plan is now to open the feature
   window on Monday and start working toward a 7.80.0 release in November.

 - AAAAAAAAA signed up for curl support.

 - Had a meeting with ZZZZZZZZ on Friday about support for
   [tiny-curl](https://curl.se/tiny/) on multiple RTOSes. Seems doable and
   fun!

 - Willy Tarreau of HAProxy fame
   [tweeted](https://twitter.com/WillyTarreau/status/1441051288997924870)
   about their working adding HTTP/3 support and yes, curl was mentioned.

 - The McAfee product "ENS for Windows" obviously uses libcurl because they
   published a [Security
   Bulletin](https://kc.mcafee.com/corporate/index?page=content&id=SB10367)
   mentioning libcurl upgrades. A little puzzling they claim at least one of
   the fixed curl flaws to be "critical" which made me curious... but there's
   a lack of details.

 - I got a few ["curl
   contributor"](https://twitter.com/bagder/status/1440578821242036237) mugs
   sent over from wolfSSL HQ

 - I got myself a ["maintainer maintainer maintainer"
   tshirt](https://twitter.com/bagder/status/1439984643424538628) from the
   Changelog podcast team.

 - I got more "loot" from GitHub, including [this fancy
   mug](https://twitter.com/bagder/status/1440026341026537491).

## Blog posts

 - [curl 7.79.1 – patched up and ready](https://daniel.haxx.se/blog/2021/09/22/curl-7-79-1-patched-up-and-ready/)
 - [curl joins the reborn IBB bug-bounty program](https://daniel.haxx.se/blog/2021/09/23/curl-joins-the-reborn-ibb-bug-bounty-program/)

## Coming up

 - curl feature window opens Monday, I'm expecting to mostly work with PR
   merges. Big and small.
 - there's a twenty year anniversary tomorrow that I'll blog about

## Feedback

[Comment here](https://github.com/bagder/log/discussions)



# September 17, 2021

## Happened this week

 - Had a great meeting with XXXXXXX. They sound very positive and we're on
   track for a support contract.

 - I shipped [curl 7.79.0](https://curl.se/changes.html#7_79_0) on Wednesday,
   did the [release presentation video](https://youtu.be/1y7BR0LZEuM) and it
   felt great - no less than three security advisories were also published in
   association with the release. About 24 hours later, we got a serious enough
   bug-report on HTTP/2 code filed that made me decide we can't wait a full
   release cycle with this and we need a patch release asap. Next Wednesday is
   now planned to be come 7.79.1 day. We will also merge other bug-fixes that
   make sense that we manage to come up with in time.

 - I did a recording of my 'just curl it' presentation for Tuesday at WebExpo.
   It'll still be broadcasted live and I will be there (online) to do the Q&A
   after the talk.

 - Tweaked the
   [vulns-per-year](https://curl.se/dashboard1.html#vulns-per-year) graph in
   the curl dashboard to better visualize when vulnerabilities were introduced
   in the code vs when they were fixed. I also added a "man pages" graph that
   will show up for the first time tomorrow in the dashboard.

 - I took the subject of [Above and beyond 32
   protocols](https://curl.se/mail/lib-2021-09/0029.html) to the mailing
   list. It primarily concerns a bitmask in the API that is about to get full
   and how to handle growing it above 32 bits in size. [The
   conclusion](https://curl.se/mail/lib-2021-09/0051.html) is probably that we
   will add a replacement option that uses a 64 bit data type when the day
   comes and we need to.

 - Amusement (A): Fabien Benetou posted a [picture on
   twitter](https://twitter.com/utopiah/status/1438863280630648834) with
   license information from his Harman Kardon Enchant speakers. It shows curl
   being used but they managed to mess up both the name of curl and the link.
   Weirdly enough, they link to an (outdated) URL for a podcast episode that I
   participated in back in 2016! [Working
   link](https://ma.ttias.be/syscast/4-curl-libcurl-future-web-daniel-stenberg/)

 - Amusement (B): I got an email about [someone wanting my help to fix a bug in
   a PS5 game](https://twitter.com/bagder/status/1437087731767721994).

## Blog posts

 - [Heading towards curl eight](https://daniel.haxx.se/blog/2021/09/13/heading-towards-curl-eight/)
 - [curl 7.79.0 – secure local cookies](https://daniel.haxx.se/blog/2021/09/15/curl-7-79-0-secure-local-cookies/)
 - [You wanted WebSockets?](https://daniel.haxx.se/blog/2021/09/16/you-wanted-websockets/)

## Coming up

 - On Tuesday the 21st: [just curl
   it](https://www.webexpo.net/prague2021/talk/just-curl-it) on WebExpo in
   Prague.
 - On Wednesday the 22nd: curl 7.79.1 release.

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# September 10, 2021

## Happened this week

 - Got more hyper issues reported. Turns out my h2 testings with it has been
   very thin so far and curl+hyper doesn't properly send the correct set of
   psuedo headers, which makes HTTP/2 requests fail against servers that are
   not very liberal in what they accept.

 - [The Rustacean Station Podcast
   #35](https://rustacean-station.org/episode/035-daniel-stenberg/) was
   published featuring me as a guest. A podcast episode about rust in curl and
   related stuff.

 - I was contacted by a lawyer who seeked my help and I have agreed to serve
   as an "exepert witness" in a Swedish web scraping court case that is due to
   go to court in mid October. I might reveal further details on this after
   I've done my part.

 - The transition of servers and services from our old physical server over to
   our new VPS is now *very* close to done. At this time there's only one
   single website left on the old hardware. `libssh2.org` still waits for a
   DNS update, but [www.libssh2.org](https://www.libssh2.org/) has moved so
   I've made the first name redirect to the later for now to better survive a
   potential HW crash before the DNS gets updated...

 - We ran [rockbox.org](https://rockbox.org)'s DNS up until now but it has now
   finally been handed over to the successors.

 - It has been a very long time coming, but I finally registered
   [c-ares.org](https://c-ares.org) and moved over the c-ares website to that
   domain. The former host `c-ares.haxx.se` will now simply redirect to the
   new name.

 - We got **two more** "last minute" security problems reported for curl for
   the pending next release. Confirmed, patched confirmed, CVEs allocated,
   things are progressing. All in all now at three CVEs in the coming release.

 - Another podcast that I participated in was published: the Popcast. The
   episode is called [total
   recurl](https://popcast-d9f7b6dc.simplecast.com/episodes/episode-81-total-recurl-with-curl-founder-daniel-stenberg). (This
   one was recorded earlier this summer.)

 - I moved most contents of my personal website
   [daniel.haxx.se](https://daniel.haxx.se/) over to get stored in git on
   github for easier maintenance.

## Blog posts

 - [Making world-class docs takes effort](https://daniel.haxx.se/blog/2021/09/04/making-world-class-docs-takes-effort/)

## Coming up

 - meeting with XXXXXXXX on Tuesday
 - need to come up with a few curl webinar topics for the autum...
 - Next week is **release week**. curl 7.79.0 is shipping on Wednesday.

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# September 3, 2021

## Happened this week

 - Did more work on hyper. Now at 64 disabled tests remaining to
   fix. Primarily I fixed how libcurl does Transfer-Encoding in the presence
   of Content-Length headers, as it was previously done wrongly. I then got a
   little stuck on NTLM with CONNECT to a proxy but I've figured out roughly
   what's wrong and that needs to be done. It's just a little complicated.

 - Moved a lot of mailing lists from cool.haxx.se to lists.haxx.se as a step
   in the shutting down of the old dying server. The libssh2 website is the
   last one to get transitioned and it is now in progress.

 - Extended the curl man page with examples - for every single command line
   option - and I'm working on polishing up examples and more in the libcurl
   option man pages.

 - Got an idea for curl's 25th birthday: [curl
   v8](https://curl.se/mail/lib-2021-09/0009.html)

 - My talk at netnod tech meeting on October 13 was announced: [curl is everywhere](https://www.netnod.se/netnod-events/netnod-tech-meeeting-2021-1/agenda)

 - Found myself listed on [the weirdest
   website](https://www.celebsagewiki.com/daniel-stenberg)

 - I put this weekly report up on github and made it [available to the
   world](https://bagder.github.io/log/) - I will edit out private data and
   names from the public version.

## Blog posts

 - working on a (curl) docs post
 - working on a post-quantum curl post

## Coming up

 - More hyper work to do.

## Comments

If you have any comments, reactions or questions. [Start a discussion thread](https://github.com/bagder/log/discussions).

# August 27, 2021

## Happened this week

 - Did more work on hyper. Now at only 73 disabled tests remaining to fix.
 - Had meeting with XXXXXXX about tiny curl
 - Preparing for post-quantum curl and related blog post
 - Worked on moving a few mailing lists to new host. Many more to come.
 - Declined to appear physically at WebExpo in September, will do a video
   presentation about [curl on September
   21](https://www.webexpo.net/prague2021/talk/just-curl-it).
 - The WebSockets API discussions have faded but what we have now in the wiki
   is a design that might just work good enough for an initial take on
   supporting this protocol. If/when the next step will be taken I'm not
   sure.

## Blog posts
 - none

## Coming up
 - More services to move so that I can finally shut down my old server
 - More hyper work to do, and I figured out problems with transfer-encoding
   in curl I should address. Will also be good for the hyper test status.
 - It would be fun to get back to fix some of the worst HTTP/3 bugs that
   have now started to pile up

# August 20, 2021

## Happened this week
 - Entered feature freeze period for curl for pending release (Sep 15th)
 - Working slowly on improving 1xx response handling with hyper. At "just" 93
   remaining tests disabled for hyper builds
 - kicked off debugging-work on Android with XXXXXXX in a productive meeting

## Blog posts
 - [a GitHub Star](]https://daniel.haxx.se/blog/2021/08/11/a-github-star/)
 - [early me caught on TV](https://daniel.haxx.se/blog/2021/08/19/early-me-caught-on-tv/)

## Coming up
 - More debugging with XXXXXXX
 - Fix more tests to work with hyper
