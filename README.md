# Daniel's weekly report

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
saying that a user couldn't changed the `:scheme` pseudo header when curl uses
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

My plan to go much further use this script output to generate a "coverage
matrix" or something in that style to better help us see what configure
outputs we use and don't use in tests etc. This, in order to help us spot if
there are any obvious "white spots" that we should make sure to add builds
for, or maybe even to detect duplicates - builds that are identical or almost
identical and therefore don't really bring any additional value.

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

# Older weekly reports

- [January 2022](January-2022.md)
- [December 2021](December-2021.md)
- [November 2021](November-2021.md)
- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
