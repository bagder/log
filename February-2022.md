# Daniel's weekly report

# February 25, 2022

## Happened this week

### headers API v2

I posted my second version of the [HTTP header access
API](https://github.com/curl/curl/wiki/get-headers-v2) proposal. After
[feedback](https://github.com/curl/curl/discussions/8496), I have improved it
a bit further and I think we might be settling in on a design now to move
forward with. I think the next step is writing a first implementation and
create man pages for the two functions from the proposal wiki. Then let people
try that out and perhaps tweak the APIs further.

It's not too late for you to check it out and tell us what you think!

### hyper test inventory

I still haven't made HTTP/2 multiplexing work with hyper. I get strange frame
size errors and I'm a little stuck in the debugging of that (and I filed [an
issue on hyper](https://github.com/hyperium/hyper/issues/2761)). In the mean
time, I went over the remaining tests that are still disabled for hyper and
took notes what they test. See the [hyper wiki
page](https://github.com/curl/curl/wiki/Hyper) for the details. I think one
way forward might be to document a few of those things as "known restrictions"
as "not supported with hyper".

### Remove output on error

After some initial discussions on [IRC](https://curl.se/docs/irc.html), I
wrote up a quick PR to introduce a
[--remove-on-error](https://github.com/curl/curl/pull/8503) command line
option. This option tells curl to remove any downloaded file if it returns
error, to avoid leaving leftovers and incomplete files. Especially useful when
doing (many) parallel transfers I think.

This might land in git once the feature window opens again. Planned for March
10.

### localization

David Hu brought a suggestion that
[localization](https://github.com/curl/curl/discussions/8499) could improve
curl as it would make it speak user's local language instead of only
English. As Dan Fandrich replied in the thread: it has taken almost 24 years
for someone to finally suggest this! I'm personally not terribly eager to work
on localization as I foresee a future with always incomplete translations. But
I'm not against the idea. If someone wants to drive it.

### msh3

I assisted Nick Banks a little this week when [he made curl use
msh3](https://github.com/nibanks/curl/pull/1) for HTTP/3. msh3 is the
Microsoft HTTP/3 library built on top of the msquic Microsoft QUIC
library. The implementation is maybe still a little rough, but I've seen it
download HTTP/3 content.

Now, I like the prospect of having three backends in curl for HTTP/3 as we're
working on having two for HTTP/2...

### docker

The "pull counter" for [the official curl docker
image](https://hub.docker.com/r/curlimages/curl) has now officially surpassed
4 billion, and while doing it the rate was at 60-70 pulls/second.

Bonus: watch Jim Fuller's presentation from 2020 titled [The First 10M Pulls:
Building The Official Curl Image for Docker
Hub](https://youtu.be/lZreoYmoMHM).

### curling in the Olympics

Sweden won one gold (men) and two bronze medals (women + mixed double) in
[curling at the 2022 Olympics](https://en.wikipedia.org/wiki/List_of_Olympic_medalists_in_curling).

## Blog posts

- [curl on “software at scale”](https://daniel.haxx.se/blog/2022/02/25/curl-on-software-at-scale/)

## Coming up

- Vacation next week, skiing with the family. Expect me to be slow to respond
- the curl 7.82.0 release happens on March 5, delayed a few days due to the
  above mentioned ski trip

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# February 18, 2022

## Happened this week

### Azure Pipelines

Since our problems with CI jobs on Azure Pipelines continued this week, I had
a meeting on Thursday with a few friendly chaps from Microsoft in which they
explained the anti-abuse system that for unknown reasons repeatedly trigger
for our jobs. We discussed mitigations and ways to get to the bottom the
problems. Their systems and ways of working are not public so I am
deliberately vague on the details here.

Since Thursday evening, Europe time, the jobs seem to run fine on Azure
Pipelines again.

### Release delay

I decided and announced that the pending **curl 7.82.0** release will be
delayed three days and instead happen on **Saturday March 5, 2022**. This,
because I will be on vacation the week before on the day of the original
release date and I rather not do the release whilst away.

We will stick to the future release dates so the next release cycle will
therefore be 3 days shorter.

### Deprecate NPN

We have now marked NPN as subject for "deprecation" later this year (next to
NSS). This TLS extension was made for SPDY and could be used for HTTP/2 in the
early days, but was removed from Chrome and Firefox already many years ago.
There should barely be any users left of this extension in the wild.

### Roadmap 2022 webinar

I did the webinar and outlined my rough plans of what I will (maybe) work on
in curl during 2022. It should be available on Youtube as well soon. Stay
tuned.

### New CI jobs

As a result of my new scripts last week for collecting info about our existing
CI jobs in curl, I figured out that we were missing testing builds with a few
backends that we support and maintain. Said and done. We are now at a total of
101 CI jobs.

### Internals documentation

I cleaned up the [libcurl internals](https://everything.curl.dev/internals)
section of *everything curl* by moving over text from the somewhat stale
INTERALS.md document we had in the source tree to make the book the single
canonical place for this docs.

Documenting internals is always hard as by nature the internals move around
and change much more since it isn't limited by API or ABI restrictions.

## Blog posts

- [The great curl roadmap 2022 webinar](https://daniel.haxx.se/blog/2022/02/14/the-great-curl-roadmap-2022-webinar/)

## Coming up

- h2 multiplexing with hyper
- my get-headers API proposal version 2, much updated

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# February 11, 2022

## Happened this week

### Azure

Azure Pipelines causes us [grief](https://github.com/curl/curl/issues/8410)
this week. Quite unexpectedly and without any warning, all the 18 CI jobs we
run on Azure Pipelines started to insta-fail at some point early Wednesday my
time. All jobs failed immediately and said this message:

    No hosted parallelism has been purchased or granted.
    To request a free parallelism grant, please fill
    out the following form.

That is almost 18% of the total amount of CI jobs we run and it impacts how we
can proceed and merge changes.

I filled in the form and talked to friends "on the inside" about situation who
help us get the service back again that evening. I also subsequently got a
confirmation email back from Microsoft stating that my *"Free tier request was
completed"*.

Then, early Friday morning **the exact same thing happened again** and when
I'm writing this at 14:57 in the afternoon the situation remains. None of our
CI jobs run on Azure Pipelines.

### strlen

Some week ago we discussed the number of `strlen()` calls done by curl (and
most importantly libcurl) on the libcurl mailing list, and since then
especially Henrik Holst has worked on reducing the number of such
calls. Primarily by replacing them with `sizeof()` calls on static strings,
which then makes it a constant at build-time. Henrik has some more work on
this in the pipe, but at least for one use case I checked, the number of calls
has been [reduced by 33%](https://curl.se/mail/lib-2022-02/0097.html)!

### :scheme

Last week we received [a bug report](https://github.com/curl/curl/issues/8381)
saying that a user couldn't change the `:scheme` pseudo header when curl uses
HTTP/2. When I fixed that oversight, I also took the opportunity to try out a
few different custom schemes when communicating with a few h2 servers running
in the wild. It turns out not a single server I tried this with cared about
what I passed to them as `:scheme`. When I then expanded my fix to also
include HTTP/3, I tried the same experiment on a handful of public servers and
they ignored the scheme exactly the same way: I couldn't find one server that
cared about what I set the scheme to in my requests. I'm not saying this is
any particular flaw or anything, but it surprised me. It is bound to lead to
the scheme becoming useless because if it'll take time until servers care
about them, it might be too late as then there might be plenty of clients who
don't send it or send the wrong contents.

I've talked to some server implementers, both h2 and h3, and I think at least
some of them might change.

### cijobs

I spent several hours this week writing a first version of the script I call
`cijobs.pl`. The purpose of this script is to parse the configuration files of
all the CI services and jobs we have setup and output data and info about them
all in a generic way. When doing this I realized I had counted the CI jobs
wrongly. We're doing 99 jobs per commit controlled by files in git right now.

This script is just the first step, and just the first take on the first step.

My plan is to go much further and use this script output to generate a
"coverage matrix" or something in that style to better help us see what
configure options we use and don't use in tests etc. This, in order to help us
spot if there are any obvious "white spots" that we should make sure to add
builds for, or maybe even to detect duplicates - builds that are identical or
almost identical and therefore don't really bring any additional value.

### quiche

I got an excellent reproducer command line to trigger an HTTP/3 problem with
curl built to use quiche. With great help from Lucas in the quiche project, I
realized they had changed their API slightly without us having updated our
logic so the problem was no mystery at all and I could make this issue go
away.

### wolfSSL

I fixed a to me very surprising [bug in the wolfSSL
backend](https://github.com/curl/curl/pull/8431). Turns out we didn't handle
the return code from the wolfSSL SSL read function correctly. It seems like
such a fundamental problem that it is really interesting and curious that we
haven't seen problems reported with this before and it took all the time until
now to fix it! Awesome help from my wolfSSL team mates too.

We have supported wolfSSL since 2006. It started its life using the name
'yassl'.

### presentation

I did my presentation "safe code is not a coincidence" (again) on Thursday for
a Swedish company. I think the pandemic has made me better at doing online
presentations. They are certainly harder to do than doing them in meat-space,
but with a little practice I think I've improved. Who could've known that is
how it works?

### podcast

I was previously a guest at the [software at
scale](https://www.softwareatscale.dev/p/software-at-scale-42-daniel-stenberg)
podcast and that episode went public this week. We talked about curl of
course. How it is to run the project, HTTP is not an easy protocol and related
matters.

### GitHub Star

In 2021 I was [invited to the GitHub
star](https://daniel.haxx.se/blog/2021/08/11/a-github-star/)
[program](https://stars.github.com/) and this week I was informed that my
status as [a star](https://stars.github.com/profiles/bagder/) has been renewed
for 2022.

## Blog posts

- [My work on tool vs library](https://daniel.haxx.se/blog/2022/02/10/my-work-on-tool-vs-library/)

## Coming up

- CI job coverage analysis
- curl roadmap 2022 webinar on the 17th

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# February 4, 2022

## Happened this week

- I took a deeper look at the curl code to see what legacy platforms we have
  A) (partial) support for, that is B) non-trivial in additional size and C)
  likely to not work anymore and D) probably aren't many current users left
  around. By the end of the week I had removed the last remaining traces of
  support for such a lovely set of platforms such as: Netware, vxWorks and
  TPF. With TPF we could also rip out the last traces of support for non-ASCII
  platforms (EBCDIC really) which consequentially made even more code get
  "slashed". All in all, a few thousand lines of negative delta. And in some
  cases much easier-to-follow code flows!

- I merged the PR that brings the `--json` command line option and I blogged
  about it and how it works.

- On Wednesday we entered [Feature
  freeze](https://curl.se/dev/feature-window.html) for curl and the next
  pending release. We will now only merge bug-fixes into the master branch
  until 7.82.0 ships on March 2, 2022.

- I did an online presentation called "safe code is not a coincidence" for a
  Swedish company on Thursday. It went well and felt appreciated. The topic is
  based on experiences and practices from the curl project of course.

- I continued to move CI jobs off of Zuul CI over to other services. As a
  result, Zuul is now number three in the most-CI-jobs-for-curl ranking, with
  GitHub Actions being #1 and Appveyor #2.

## Blog posts

- [1,000 commit authors](https://daniel.haxx.se/blog/2022/01/30/1000-commit-authors/)
- [curl with rust](https://daniel.haxx.se/blog/2022/02/01/curl-with-rust/)
- [curl dash-dash-json](https://daniel.haxx.se/blog/2022/02/02/curl-dash-dash-json/)

## Coming up

- Move over more CI jobs from Zuul CI to other services
- curl roadmap 2022, time to start making some slides. Webinar planned for the 17th
- Working the header API proposal, maybe, as it didn't happen this week
- Doing the safe code presentation again, for another company

## Feedback

[Comment here](https://github.com/bagder/log/discussions)
