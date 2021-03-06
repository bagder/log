# Daniel's weekly report

# November 26, 2021

## Happened this week

- Possibly the best this week was the [callout I did on
  Twitter](https://twitter.com/bagder/status/1462094197448716293): *"friends
  at @Microsoft: we keep getting reports from users about your outdated curl
  version in Windows 10 and Windows 11. They are (rightfully) concerned that
  you don't fix known security problems. How about an upgrade?"* which after a
  few turns found the exact right person (Dustin Howett at Microsoft) who
  graciously
  [replied](https://twitter.com/DHowett/status/1462156074824482823): *"All
  that to say: I’m sorry, and we’ll do better in the future. As a huge fan of
  curl, I was so happy to see it end up in Windows… and now as the owner of
  that integration, I’m compelled to make sure we’re doing it right. Thanks
  for everything!"* I couldn't wish for a better response!

- Another fun adventure of the week kicked off with **oss-fuzz** reporting a
  [Heap-buffer-overflow in curl](https://github.com/curl/curl/issues/8041),
  but none of us managed to reproduce it and we couldn't at all understand it.
  This made us file a bug report in oss-fuzz about this being a [Suspected
  false positive](https://github.com/google/oss-fuzz/issues/6879) and thanks
  to very quick action there it was soon be confirmed and fixed. Well,
  "fixed", maybe because for some reason the deployment of the fix has shown
  to take a while and in the mean time we seem to have received two more
  oss-fuzz false positive reports in the same style. I've been asked to "hold
  my breath" until after this coming weekend so let's hope we aren't drowned
  in more of these before then...

- This week's libcurl sighting: [Baldur's Gate
  3](https://twitter.com/AkhlisRO/status/1463961095408869386) uses it.

- I looked closer at the problem with hyper changing the order of delivered
  incoming headers if they use the same name, and I've decided that the API
  currently provided for me to "untangle" them is insufficient. The API right
  now offers all headers in a single memory blob, for me to parse and figure
  out. But if the point of using hyper is to lean more on a HTTP parser
  written in rust, I feel it goes against that concept pretty strongly if we
  would then parse all the headers **anyway** using C, for the purpose of
  keeping the libcurl behavior. This now puts us in a position where we're a
  bit blocked and I don't know how to move this forward.

- My request for HTTP/1.1 trailer support in hyper was accepted, but there's
  no new code or API or anything available yet for me to work with.

- This week's share of hair-tearing has happened in [PR
  8035](https://github.com/curl/curl/pull/8035) and it still isn't solved.  It
  is a minor change in how curl scans for the existence of a `.curlrc` and
  `.ssh/known_hosts` (ie in different places that could be considered "home"),
  but for some reason the CI runs on some Windows builds seem to crash and
  I've so far failed to understand it. And I can't run or reproduce the
  problem on my own.

- I made editing the website simpler by making sure we can run a local copy
  under the name `curl.local`. See that
  [README.md](https://github.com/curl/curl-www/blob/master/README.md) for
  details. I also added a first basic CI job for the website to maybe reduce
  the risk that we break it when we change stuff. I also wanted to make the CI
  provide browsable versions of HTML files to make it possible to see how a PR
  will render when merged, but I haven't figured out how to do that yet...

- I added a CI job to [everything curl](https://everything.curl.dev/) that
  runs [proselint](http://proselint.com/) on the entire book, which should
  help us keep language decent even when we go forward.

## Blog posts

No posts this week!

## Coming up

- Fix more tests to work with hyper

# November 19, 2021

## Happened this week

- Opened the [feature window for
  curl](https://curl.se/dev/feature-window.html) on Monday. Started merging
  things that have been queued up...

- I reached 16,000 commits in curl's source code repo just after I posted my
  weekly report last week.

- I signed up to participate in the panel at the free online event coming on
  December 14 called [The Future of Open Source: Is It
  Sustainable?](https://sentry.io/resources/the-future-of-open-source-is-it-sustainable/)
  by [Sentry](https://sentry.io/)!

- Tuesday: I did a curl presentation - in person - for a Stockholm based
  company. Even managed to cram in some HTTP/3 details and had a good time
  with a range of good and intersting questions and follow-up discussions. The
  best kind of event!

- While working on the slides for my webinar this week (which I had postponed
  for far too long this time), I had libreoffice crash on me repeatedly so
  many times I finally gave up on it. For good. I've created all my
  presentations in libreoffice for many years, but with this last streak of
  hard crashes I'm now done. It has always been "crashy", but with some recent
  update it became totally unusable for me. Fortunately, exporting from
  libreoffice into powerpoint and importing into Google slides worked pretty
  good so I at least didn't have to redo all the work.

- Thursday: I did a curl webinar, on [the release and post
  quantum](https://daniel.haxx.se/blog/2021/11/16/curl-release-webinar-featuring-post-quantum-curl/) -
  the video recording has not yet come online but I will update the blog post
  with it as soon as it does.

- Participated on a podcast recording Thursday. We talked curl details and
  experiences in a way I think I haven't talked too much before. For example
  *"Why do you think HTTP is a complex protocol?"*.  I'll let you know when it
  becomes available for listening. [older podcast
  participations](https://daniel.haxx.se/podcasts.html)

- I've worked on cleaning up and overhauling [everything
  curl](https://everything.curl.dev/) quite a bit this week. Triggered mostly
  by me browsing it and I found a few outdated details. Added a few sections,
  refreshed some and restructed a few others. I have more ideas of areas I
  could go over to improve a bit more soon as well. The book is now at 75,000
  words. I'm missing a good "get libcurl for Windows" section so I asked about
  suggestions for it [on the mailing
  list](https://curl.se/mail/lib-2021-11/0037.html).

- I want to offer the regular curl [man
  page](https://curl.se/docs/manpage.html) on the webpage in an additinal
  alternate way: with each command line option in its own invidual webpage. [I
  posted to curl-users](https://curl.se/mail/archive-2021-11/0004.html) asking
  for feedback with two sample images showing what it could look like. Didn't
  get very productive responses so far...

- This week in curl+hyper land, I've looked at test cases that use HTTP
  trailers (for example [test
  1417](https://github.com/curl/curl/blob/master/tests/data/test1417)). I
  found no support in the current hyper API for them so I've submitted a
  [feature-request](https://github.com/hyperium/hyper/issues/2699). I also
  fixed haproxyprotocol suppport.

- I did some preliminary attempts to build nghttpx with HTTP/3 support but ran
  into build problems I haven't yet resolved.

## Blog posts

- [16000 curl commits](https://daniel.haxx.se/blog/2021/11/12/16000-curl-commmits/)
- [Fun multipart/form-data inconsistencies](https://daniel.haxx.se/blog/2021/11/13/fun-multipart-form-data-inconsistencies/)
- [cURL Release Webinar – Featuring Post Quantum cURL](https://daniel.haxx.se/blog/2021/11/16/curl-release-webinar-featuring-post-quantum-curl/)
- [Free Apple support](https://daniel.haxx.se/blog/2021/11/18/free-apple-support/)

## Coming up

- check what more hyper features that are lacking for remaining test cases and
  submit feature-reuqests for them
- make nghttpx work for HTTP/3 and create a first set of HTTP/3 tests for curl

## Advertisment

- Buy [curl support](https://curl.se/support.html) from me via wolfSSL!
  Offloads your engineers to do other things and leaves the curl work to the
  experts. Win-win.

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# November 12, 2021

## Happened this week

- Put together and shipped curl 7.80.0 and there was much rejoicing. See the
  blog post for details.

- I missed the OpenSSL QUIC side-meeting at the IETF but I enjoyed watching
  [the recording](https://www.youtube.com/watch?v=YVBBpsZJUcs).

- Had a meeting with new potential customer about getting sponsorship for
  implementing feature NNNNNNN. If this lands, it'll give me something to work
  on **months** ahead...

- I tweeted about the current HTTPbis work on
  [QUERY](https://www.ietf.org/archive/id/draft-ietf-httpbis-safe-method-w-body-02.html)
  as a new HTTP method, sort of a "GET with a body", and it got a lot of
  attention and follow-up interest. HTTPbis is the HTTP working group within
  IETF.

- The [official docker image for
  curl](https://hub.docker.com/r/curlimages/curl) surpassed 3 **billion**
  pulls. The current rate is somewhere around 140 pulls/second.

- [ngtcp2](https://packages.debian.org/source/sid/ngtcp2) built against GnuTLS
  showed up in Debian sid. You can build curl's HTTP/3 support with this!

## Blog posts

- [curl 7.80.0 post quantum](https://daniel.haxx.se/blog/2021/11/10/curl-7-80-0-post-quantum/)
- [The curl v8 plan](https://daniel.haxx.se/blog/2021/11/11/the-curl-v8-plan/)
- [My first 25 years of HTTP](https://daniel.haxx.se/blog/2021/11/11/my-first-25-years-of-http/)

## Coming up

- The curl feature window reopens Monday
- A curl presentation Tuesday for a Stockholm based company
- Podast episode recording on Thursday
- Webinar on the curl release and post quantum on Thursday (details pending)

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# November 5, 2021

## Happened this week

- Discussed [English
  contractions](https://twitter.com/bagder/status/1455659677400829955) being
  good or bad on twitter after I filed [my PR to reduce the
  amount](https://github.com/curl/curl/pull/7930) in curl documentation. This
  followed [my previous PR that removed 230 instances of the word
  'very'](https://github.com/curl/curl/pull/7936) from the same set of
  documentation. I believe there is always room to discuss and improve
  documentation language.

- I did an internal presentation about libcurl and
  [tiny-curl](https://curl.se/tiny/) for wolfSSL colleagues.

- We celebrated `curl.se` (the domain) having been in use for a year
  now. Wohoo!

- I started looking at using nghttpx as a proxy for some first HTTP/3 tests in
  curl. We already use it for HTTP/2 tests, so it could be handy to reuse the
  same tool. I provided [a pull request to
  nghttp2](https://github.com/nghttp2/nghttp2/pull/1636) to make sure we can
  detect if it was built with h3 support enabled. It was (improved and)
  merged. Early days still.

- The rustls integration in curl needs some attention as upstream has modified
  the C API recently. While checking this out, I noticed that the
  [rustls_version was documently
  wrongly](https://github.com/rustls/rustls-ffi/issues/168), but it was
  [fixed](https://github.com/rustls/rustls-ffi/pull/171) immediately.

## Blog posts

- no blog post this week!

## Coming up

- curl 7.80.0 release

## Feedback

[Comment here](https://github.com/bagder/log/discussions)
