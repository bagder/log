# Daniel's weekly report

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

 - We ran [rockbox.org](https://rockox.org)'s DNS up until now but it has now
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
