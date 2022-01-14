# Daniel's weekly report

# January 14, 2022

## Happened this week

- The curl [feature window](https://curl.se/dev/feature-window.html) is now
  open and we've started to merge outstanding pull-requests for new features.
  This also means that the next curl release is now going to be called
  **7.82.0**.

- The report on [URL parser
  confusion](https://security.claroty.com/URLparserconfusion) that I have I
  mentioned before went public on Monday. It discusses problems and
  inconsistencies among URL parsers that can lead to vulnerabilities. I also
  joiend Snyk's [live stream](https://www.twitch.tv/videos/1260182192) and
  talked about the report and the topic. I also wrote a separate blog post
  about it, see below.

- Microsoft took a big step forward this week and shipped an upgrade to curl
  for Windows. They had stalled on version 7.55.1 for years and now they took
  a giant leap in one go straight up to **7.79.1**. Dustin Howett said they
  intend to [keep up-to-date
  better](https://twitter.com/DHowett/status/1481302347552862211) going
  forward.
  
- In Microsoft's [upgrade
  note](https://msrc.microsoft.com/update-guide/en-US/vulnerability/CVE-2021-22947),
  they specifically highlight that they've addressed
  [CVE-2021-22947](https://curl.se/docs/CVE-2021-22947.html) but they also
  confusingly call that problem a "Remote Code Execution Vulnerability" -
  which it isn't. After some back-channel talk, it has been explained that
  they fixed a whole range of problems with that upgrade and it includes one
  RCE. This seems reasonable, as we list quite a few [known vulnerabilities in
  7.55.1](https://curl.se/docs/vuln-7.55.1.html). **35** to be exact.

- At wolfSSL we have started the year by internally discussing **the curl 2022
  Roadmap** or more specifically what I will work on in curl this year. I took
  the subject to the mailing lists and I also got a lot of feedback on my
  Twitter question for [lessons from curl
  alternatives](https://twitter.com/bagder/status/1481186883560476674). We are
  going to customers starting next week and I will most likely do a webinar on
  the topic maybe early February.

- I did an internal curl presentation at [wolfSSL](https://www.wolfssl.com/)
  since we have quite a few new faces at the company over the last
  year. What's curl, what does it do, existing customers, how do we (want to)
  sell curl and something about the possible roadmap 2022. In the big wolfSSL
  family of libraries and products, curl is certainly the little brother
  business-wise. Room to grow.

- Our friends in the [quiche project](https://github.com/cloudflare/quiche)
  [landed a changed](https://github.com/cloudflare/quiche/pull/1122) that
  brought the `quiche_conn_peer_cert()` function that would allow us to verify
  the server certificate when doing QUIC connections (for HTTP/3) with this
  library. Ironically though, it still turned out inadequate for curl's
  purposes and we instead took [a different
  route](https://github.com/curl/curl/pull/8275) when Alessandro Ghedini
  stepped up and took us a lot closer to the goal. Without using that new
  function.

- Vaxxed v3.

## Blog posts

- [Don’t mix URL parsers](https://daniel.haxx.se/blog/2022/01/10/dont-mix-url-parsers/)

## Coming up

- More PR review and merging.
- A libssh2 release is due and it might happen this coming week
- curl roadmap 2022
- A blog post around [the OSS pyramid](https://twitter.com/bagder/status/1481938497728569345)

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# January 7, 2022

## Happened this week

- Because I had some time off during Xmas I didn't do any weekly report last
  week and therefore this edition might include stuff I did last week when I
  was supposed to not do much.
  
- On January 5 we released curl 7.81.0, and I got to be the release shepherd
  for the 205th curl release ever. There have been some issues reported on
  this version, in particular some annoying build related quirks, but so far
  none of them have been deemed serious enough to warrant any follow-up patch
  release. It looks like we can open the feature windows next week and plan
  for a 7.82.0 release for **March 2** - precisely according to the schedule.
  
- I have brought up the discussion about "curl roadmap 2022" on the mailing
  lists as well as [on
  Twitter](https://twitter.com/bagder/status/1479216791998058498) in order to
  listen in on what people are thinking about and want for curl these days. I
  hope to put together a 2022 roadmap that at least outlines what **I** plan to
  work on for curl this year. It is also intended to highlight the fact that
  paying customers/companies of mine can affect this. Get in touch!
  
- Almost every single downstream curl packager has its own set of custom
  patches applied. Many of those changes are just patches that affect
  particular details in the build and are not details we would like to modify
  in the project's upstream code. After I did a closer inspection of the
  patches used by Debian, FreeBSD and msys it is also clear that there are
  functional changes all over that the downstreams haven't submitted to us. In
  most cases they also ship and get applied without much explanations or
  documentation making it hard for us to do anything about them. I assume the
  patches *are* or *were* better motivated at some point.
  
- I have slowly started to move CI jobs away from Zuul CI over to other
  services. When Travis ["went
  rogue"](https://daniel.haxx.se/blog/2021/06/14/bye-bye-travis-ci/) last
  summer, we moved almost all of those CI jobs over to Zuul CI and we were
  happy having managed the shutdown in such an elegant and swift manner. At
  the most, we had 31 different CI jobs running on Zuul (out of the about 100
  jobs we run in total). Over time however, it has turned out that Zuul's
  integration with GitHub is so flawed and that builds frequently don't even
  show up in Zuul's UI that I have felt forced to decide that they are not a
  preferred service either. It's not any alarming problem but I plan to pick a
  few jobs every now and then and get them moved over to run on other services
  instead. Feel free to help me out with this.

- Let me tell you about my hack of the week to increase my productivity: I've
  now created a build script that replaces my alias (`b`) I've been using for
  building curl. The previous alias would do `make -C $HOME/src/curl -sj7`
  just as a convenient shortcut (it uses `-s7` only to make my video streaming
  performance get less affected when I do live-coding sessions). The
  replacement now has an additional tweak: it also scans *modified* files to
  verify that the copyright year ranges are correct. curl's copyright scan
  script is otherwise too slow to run against *all* files in every build
  command. The complete script looks like this:

~~~shell
#!/bin/sh
cd /home/daniel/src/curl
files=$(git diff origin/master --name-only)
if test -n "$files"; then
    ./scripts/copyright.pl $files
    res=$?
    if test $res != 0; then
        exit 2
    fi
fi

make -sj7
~~~

## Blog posts

- [curl 7.81.0 – more
  percent](https://daniel.haxx.se/blog/2022/01/05/curl-7-81-0-more-percent/)

## Coming up

- The curl feature window opens on Monday the 10th. There are plenty of pull-
  requests already waiting to get merged once that happens.
- There will be a report published on newly discovered URL problems. The
  report comes from people at Snyk and Claroty but I've read it and given it
  my thumbs up. I'll do my own blog post about it too.
- There will be a live-streamed discussion about the above mentioned URL
  report that happens on Tuesday 15:00 UTC on
  [Twitch](https://www.twitch.tv/snyklive) where I will participate.
- I will continue to improve the HTTP/3 support. I want to get to fixing [cert
  verification for curl +
  quiche](https://github.com/curl/curl/issues/8173). If out friends in the
  quiche project delivers, this might be a fine topic for me to also do a
  live-streamed session with. Follow me on
  [Twitter](https://twitter.com/bagder) or
  [Twitch](https://www.twitch.tv/curlhacker) if you don't want to miss it.

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# Older weekly reports

- [December 2021](December-2021.md)
- [November 2021](November-2021.md)
- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
