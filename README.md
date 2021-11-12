# Daniel's weekly report

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

# Older reports

- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
