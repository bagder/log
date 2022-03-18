# Daniel's weekly report

# March 18, 2022

## Happened this week

### headers

I cheated a little and started working on implementing the new proposed header
API for libcurl already last weekend. I've then continued and spent a
majority of my curl time this week on it.

While we had a pretty good proposal already before I wrote any code for it, it
was of course not good enough once I started to actually get into the
specifics and details around how it should work and how to provide all the
headers in the most flexible and reliable way for applications using
libcurl. I think I refined the API at least 4 or 5 times during the week,
mostly because working on the code made me think harder about the problems but
also because of good feedback from contributors when I got back with my new
lessons learned. The [get headers v2 wiki
page](https://github.com/curl/curl/wiki/get-headers-v2) has been updated
accordingly to make it easier for outsiders to see the API. (I will remove
that wiki page once the man pages get merged into git so that we rather have
the API docs in a single place.)

This API work is almost complete and still lives in [PR 8593](https://github.com/curl/curl/pull/8593).

### cmdline header options

While working on the header API I wanted to add another test case and I
figured it would be easier to do that if I first made the command line tool
able to output the headers. Using the tool in test cases is often easier and
quicker than testing libcurl functions.

This was also a great first use case for the new header API. It took me less
than an hour of work to make a first shot at providing headers for command
line users with two new extensions to the `-w` option. Then it took me a
little longer to figure out JSON syntax and how to format the output properly.

Right now, this is how they work:

**Individual headers**
~~~
$ curl -w '%header{date}\n' -o savefile curl.se
Thu, 17 Mar 2022 16:59:24 GMT
~~~

**All headers output as JSON**
~~~
$ curl -sw '%{header_json}\n' -o savefile curl.se | jq
{
  "Date": [
    "Tue, 09 Nov 2010 14:49:00 GMT"
  ],
  "Server": [
    "test-server/fake"
  ],
  "Last-Modified": [
    "Tue, 13 Jun 2000 12:10:00 GMT"
  ],
  "ETag": [
    "\"21025-dc7-39462498\""
  ],
  "Accept-Ranges": [
    "bytes"
  ],
  "Set-Cookie": [
    "firstcookie=want; path=/",
    "2cookie=want; path=/",
    "cookie3=want; path=/"
  ],
  "Content-Length": [
    "6"
  ],
  "Connection": [
    "close"
  ]
}
~~~

### LWN

My [blog post about curl-minimal](https://daniel.haxx.se/blog/2022/03/16/fedora-and-curl-minimal/) made it into a [quote on lwn.net](https://lwn.net/Articles/888098/):

*It is really hard for packagers to know what curl features that are used and
not used. There simply is no way to find out, besides shipping a version and
listening to the screams of users in pain when things break. It will also
force them into line-drawing decisions such as “only N users seem to use
feature Z so let’s keep that in the full package” and figuring out the N
number is a fuzzy estimate at best.*

### Mystery CVE

Apple [posted a macOS security
update](https://support.apple.com/en-us/HT213183) in which they refer to curl
CVE that doesn't exist: **CVE-2022-22623**. Several sites have already
speculated wildly what this flaw is. I'm in touch with the mother-ship now to
figure out what they actually meant.

### 24,000 stars

Just days before curl's 24th birthday we reached 24,000 stars on the [curl
GitHub repository](https://github.com/curl/curl). Seems fitting.

### Webinar

I ran a webinar called [getting started with
libcurl](https://daniel.haxx.se/blog/2022/03/15/webinar-getting-started-with-libcurl/)
on Thursday. The video recording is not yet available.

### Sean's hyper blog post

Sean McArthur blogged [Help stabilize hyper in curl](https://seanmonstar.com/post/678895803144830976/help-stabilize-hyper-in-curl) - about how help out to get the final tests in curl still don't worth with hyper fixed.

### Podcast recording

I recorded a podcast episode with the awesome hosts of the podcast [Trevlig
mjukvara](https://trevligmjukvara.se/) - in Swedish. Supposed to be published
soon.

### Podcast publication

[Cybersecurity: Amplified and Intensified #57](https://anchor.fm/amplifiedandintensified/episodes/57---Daniel-Stenberg-Creator-of-cURL-and-libcurl-e1fdq43) was published, where I guested the podcast and talked curl, money, open source and supply chain.

## Blog posts

- [curl no clobber](https://daniel.haxx.se/blog/2022/03/12/curl-no-clobber/)
- [webinar: getting started with libcurl](https://daniel.haxx.se/blog/2022/03/15/webinar-getting-started-with-libcurl/)
- [Fedora and curl-minimal](https://daniel.haxx.se/blog/2022/03/16/fedora-and-curl-minimal/)

## Coming up

- curl's 24th birthday
- landing PR 8593?

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


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
