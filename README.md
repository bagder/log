# Daniel's weekly report

# August 26, 2022

## curl up 2022

The agenda has been extended with details now and it is starting to look fine.

## Uncurled

I did a live presentation on Tuesday that I called
[Uncurled](https://daniel.haxx.se/blog/2022/08/18/uncurled-the-presentation/)
with me talking about what people can expect when running Open Source projects
and how I think you can run such proejcts (there's a video on the page the
link takes you). Of course based a lot on the contents of my
[book](https://un.curl.dev/) with the same name.

As a direct result of questions I received and topics that was brought to the
top of my mind when doing this, I then extended the book with more contents in
the week. I added a few entirely new sections and enhanced a few. I also fired
up a new crontab job and now I offer a PDF version of the book, updated daily,
[here](https://daniel.haxx.se/uncurled/).

Uncurled is now 23,100 words long.

## Funding

I had a great meeting with a European organization that is interested in
funding and improving infrastructure Open Source projects, and curl meets the
criteria. We are moving forward with some ideas on how it can and should be
done so that both sides are happy and get the most out of it. Fingers
crossed. I will of course give you all more details when I can and if the
ducks end up in the right order.

## Android follow-up

Back in [April](April-2022.md) I mentioned a complicated and hard-to-debug
problem one of my customers experienced with libcurl with their large volume
app on Android. This has now finally turned out to be... not a problem in
libcurl at all, but was found to be a flaw in adjacent code. Hooray for us.

## Websockets

I am now down to only one unchecked checkbox for what I need to do in
[pull-request](https://github.com/curl/curl/pull/8995). It is looking good for
a merge when the feature window opens after the coming release.

One of the reasons there is only one checkbox left is that I have postponed a
few things to instead split up the work and to a subset of the work after the
initial release: in particular I am thinking about adjustments for the curl
tool and some more. My hope is that the initial merge will trigger some early
users to try it out and give feedback so that we can smoothen out rough
corners and perfect it that way - a in parallel with further development.

[Corellium](https://twitter.com/CorelliumHQ/status/1539277242886500353)
sponsors my WebSockets work.

## Pending release

The 210th curl release is scheduled for next week. One CVE will be announced
in assocation with the release. I will do a release video presentation live as
usual on the Wednesday.

## Blog posts

- [Increased CVE activity in curl?](https://daniel.haxx.se/blog/2022/08/22/increased-cve-activity-in-curl/)
- [What if I vanished?](https://daniel.haxx.se/blog/2022/08/24/what-if-i-vanished/)
- [curl up 2022 take 2](https://daniel.haxx.se/blog/2022/08/26/curl-up-2022-take-2/)

## Coming up

- more websockets work and polish
- curl 7.85.0 release on Aug 31

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# August 19, 2022

## Coverity

After an upgrade, the code analyzer Coverity seems to have gotten this newly
found ability to spot issues with time_t and 32 bit in the code and it
correctly identified a problematic code section we had in SFTP. Actually
present twice with minor variations, in two different backends.

## Websockets

I had another productive week of improvements to the code. Out of my list of
**25** bullet points listed in the PR that I have identified we need done
before we can consider having reached the first milestone, I have now nailed
**20** of them.

(I spent far too may hours yesterday to debug a regression in the code that
made the websockets branch break HTTP/2 upgrades.)

Note quite "there" yet, but we certainly have the foundation in place, it
seems to work decently and I will continue to fill in the remaining blanks in
the weeks to come.

If anyone has a use case for websockets support today and wants to work with
me to try out the new websockets API early, I'm very interested in getting in
touch!

[Corellium](https://twitter.com/CorelliumHQ/status/1539277242886500353)
sponsors my WebSockets work.

## Memory-leaks

I have this long-standing task to move away CI jobs from Zuul and make them
run on other services instead (because [zuul doesn't work good
enough](https://github.com/curl/curl/issues/9026)) and this week I moved
another few jobs: namely [torture
tests](https://everything.curl.dev/internals/tests/torture).

When doing this, I happened to trigger and find no less than *two* separate
memory-leaks in exit paths in the name resolver code! Fixed now.

## Everything curl

I added a whole new section to the book, explaining and describing all there
is to say about [tests](https://everything.curl.dev/internals/tests) in the
curl project.

File format, how to build tests, how to run them, debug builds, test servers,
different test kinds, CI jobs, autobuilds etc.

## curl up

I am slowly getting the [agenda](https://github.com/curl/curl-up/wiki/2022)
for curl up 2022 done and I have emailed all speakers to get their commitments
confirmed to make sure we can deliver on the promises.

There is still time and room to add more intersting stuff!

## Blog posts

- [QUIC and HTTP/3 with wolfSSL](https://daniel.haxx.se/blog/2022/08/15/quic-and-http-3-with-wolfssl/)
- [The curl release cycle](https://daniel.haxx.se/blog/2022/08/16/the-curl-release-cycle/)
- [Uncurled - the presentation](https://daniel.haxx.se/blog/2022/08/18/uncurled-the-presentation/)
- [100,000 words](https://daniel.haxx.se/blog/2022/08/19/100000-words/)

## Coming up

- more websockets work and polish
- talking up curl up
- my "uncurled" presentation

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# August 12, 2022

## Happened this week

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
