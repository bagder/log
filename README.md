# Daniel's weekly report

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
