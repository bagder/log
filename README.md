# Daniel's weekly report

# December 2, 2022

## 5-digit issue numbers

On GitHub, the curl project broke the limit and is now in the 5-digit range of
issues and pull-requests after [almost eight
years](https://daniel.haxx.se/blog/2015/03/03/curl-embracing-github-more/) of
using it as our primary "tracker".

This is of course just another number without any inherent meaning. We expect
the next 10,000 issues to go faster than the first set.

## TLS

Stefan Eissing's continued work on connection filters for curl internals made
us merge his TLS rework this week, and as a direct result of that curl now
supports HTTPS proxies with many more TLS backends than before. The notable
part of using HTTPS proxies of course being that speaking HTTPS over them
makes the transfer do double TLS.

## h3 tests

During our recent refactor work of connection and HTTP internals we managed to
accidentally break HTTP/3 support several times, because we did not have any
HTTP/3 tests running in our CI. We only verified HTTP/3 *builds* which
obviously was not good enough. This was not any surprise really, but Stefan
did good work in that area as well and now we at least have an initial test
(and framework) that verifies very basic working HTTP/3 in curl. I expect us
to extend this more going forward.

## `%{certs}`

Someone wanted to get the server certificate chain from an HTTP/3 server.
Typically users use the openssl tool for this, but it doesn't support
HTTP/3. Since libcurl already has this ability but it just isn't exposed to
the tool, it was easy to [created a draft
PR](https://github.com/curl/curl/pull/10019) to work out how this can be done
by curl's `-w` option in the future.

## Blog posts

No posts this week

## Coming up

- more of the same

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

[here](all.md)
