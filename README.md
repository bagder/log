# Daniel's weekly report

# January 7, 2021

## Happened this week

- Because I had some time off during xmas I didn't do any weekly report last
  week and therefore this edition might include stuff I did last week when I
  was supposed to not do much.
  
- On January 5 we released curl 7.81.0, and I got to be the release shepard
  for the 205th curl release ever. There have been some issues reported on
  this version, in particular some annoying build related quirks, but so far
  none of them have been deemed serious enough to warrant any follow-up patch
  release. It looks like we can open the feature windows next week and plan
  for a 7.82.0 release for **March 2** - precisely according to the schedule.
  
- I have brought up the discussion about "curl roadmap 2022" on the mailing
  lists as well as [on
  Twitter](https://twitter.com/bagder/status/1479216791998058498) in order to
  listen in on what people are thinking about and want for curl these days. I
  hope to put togeter a 2022 roadmap that at least outlines what **I** plan to
  work on for curl this year. It is also intended to highlight the fact that
  paying customers/companies of mine can affect this. Get in touch!
  
- Almost every single downstream curl packager has its own set of custom
  patches applied. Many of those changes are just patches that affects
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

- The curl feature window opens on Monday the 10th. There are plent of pull-
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
