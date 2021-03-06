
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

