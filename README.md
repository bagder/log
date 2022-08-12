# Daniel's weekly report, August 12, 2022

## vacation

It has been several weeks since I last wrote a weekly report. I had this
period of vacation mixed with a little work. It was great but now I'm back at
full speed ahead and I have spent this week working hard on shrinking the
amount of open issues and pull-requests. They had managed to grow in number
about recently but as we reach the end of this week they seem to be down to
manageable numbers again.

## feature freeze

Last week curl entered feature freeze and we are aiming for a release on
August 31, which makes the release cycle one week longer than usual this
time. It might actually result in a record number of bugfixes for a single
release if the pace keeps up.

## QUIC

Stefan Eissing landed his QUIC API work in wolfSSL this week, giving yet
another TLS library the ability to be used in a QUIC implementation. If the
plan sticks, we should soon be able to run HTTP/3 transfers with curl using
ngtcp2 powered by wolfSSL. I promise to let you know when you too can try this
out!

## IPFS

When I noticed a [tweet by
Phoronix](https://twitter.com/phoronix/status/1557302372396941312) saying
**"#IPFS Supported In FFmpeg 5.1, IPFS Devs Envision Support In More
Open-Source Project"** I decided I should just write down what I have learned
about IPFS and the use of remote HTTP gateways and how I think the use of a
default one is a bad idea. I figured that if how this works was a surprise to
me, it might also be a surprise to others.

The reaction in the ffmpeg project was instant and a
[patch](https://ffmpeg.org/pipermail/ffmpeg-devel/2022-August/299924.html) was
posted to revert the default gateway. The follow-up discussion on that mailing
list turned emotional very quickly but at least the ball is rolling now.

## websockets

I haven't worked a lot on this recently but I hope to get back up to speed and
to expand the number of tests and make sure I complete the full planned API
soon. I want to do an initial merge in the next feature window, which is open
September 5 - 28.

The feature will be marked **EXPERIMENTAL** and require a special configure
flag to get enabled to start with anyway so it should be fairly safe.

[Corellium](https://twitter.com/CorelliumHQ/status/1539277242886500353) sponsors my WebSockets work.

## Blog posts

- [How I merge PRs in curl](https://daniel.haxx.se/blog/2022/08/08/how-i-merge-prs-in-curl/)
- [IPFS and their gateways](https://daniel.haxx.se/blog/2022/08/10/ipfs-and-their-gateways/)
- [The dream of auto-detecting proxies](https://daniel.haxx.se/blog/2022/08/12/the-dream-of-auto-detecting-proxies/)

## Coming up

- websockets work
- agenda work for curl up
- create my "uncurled" presentation for the 23rd

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# Older weekly reports

[here](all.md)
