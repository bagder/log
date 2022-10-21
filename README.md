# Daniel's weekly report

# October 21, 2022

## funding

This week it was finally made public: the Sovereign Tech Fund out of Germany
is funding three separate curl projects to be done over the coming six
months. I will do one of them and Stefan Eissing steps in and will handle two
of them. I'm thrilled to be able to get this dedicated time and effort to
improve curl further the coming months.

I [blogged lots of details](https://daniel.haxx.se/blog/2022/10/19/funded-curl-improvements/) about the selected projects.

## man page

In an attempt to make the man page for the curl tool more explicit and clear
about what happens when you specify command line options more than once, I
made this piece of information mandatory for each option. This way, the
generated output clearly mentions for them all if they can be specified
multiple times etc. I had to go through all the 248 existing options in a long
tedious session to make sure that metadata is set for each of them. In the end,
the resulting man page grew with some 400 lines or so.

Since this metadata now is mandatory - leaving it out causes a build failure -
it means that when we add new command line options in the future, this
information has to be provided.

## bugfixes

We have kept up the pace of bugfixes through the last week as well and we are
now looking at a possible new project record amount of bugfixes in a single
release in the coming 7.86.0.

## security

On Monday I notified the distros@openwall mailing list about our pending CVE
announcements.

The security audit has now ended and I believe every issue they found have
been addressed now, and the single security related one is being as a CVE in
the release next week.

## oss-fuzz

We merged a whole bunch of new fuzzer code into OSS-Fuzz almost a week ago to
make it fuzz more options and more curl parsers. This was one of the direct
results of good work from Trail of Bits. I was a little scared of what that
would do to us, but to my amazement they have not triggered even a single new
report so far.

## Blog posts

- [Deviating from specs](https://daniel.haxx.se/blog/2022/10/18/deviating-from-specs/)
- [Funded curl improvements](https://daniel.haxx.se/blog/2022/10/19/funded-curl-improvements/)

## Coming up

- release preparations
- curl 7.86.0 ships on Wednesday

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# October 14, 2022

## security

Debris and tidbits from the security audit have kept me busy this week again.
Trail of Bits reported several bugs and discrepancies that we worked on
fixing. So far their work has (fortunately) only resulted in a single CVE. In
addition to the three ones reported by others, it makes a total of **four**
pending CVEs for the next release. Severity levels medium and low.

A few issues have taken a lot effort to assess the impact of, to make the call
whether they are security problems. My goal is to make sure that all known
security issues are fixed and get announced in sync with the next release and
right now that seems to hold.

Trail of bits have completed their audit now and their final report is due any
day now. We will make everything public as soon as we can - once all possibly
security-related issues have been dealt with. My early take: no major problems
found but (some) areas can be improved.

To complicate matters and my life a little extra, HackerOne decided to act up
this week: we normally use their service to request CVE Ids for issues. It is
usually convenient and seamless as the system for it is integrated with their
issue tracker. This time however, the system first denied me a new CVE last
week for one of the issues we have and then *again* this week when I tried it
again and requested a CVE for a different issue still in need of one. The
HackerOne support has always been great in the past but unfortunately they
disappointed me this time to the degree that I decided to run over and request
two CVEs directly from MITRE instead. Which worked swiftly and effectively.

I want to pre-notify the distros@openwall next week and I want the CVEs
assigned by then so that I can make sure all the documentation and records in
our end are clear.

HackerOne support still has not gotten back to me about this issue.

Counting this last batch, we are at a total of 130 CVEs assigned for curl
through-out history.

## eurorust

I talked "rust in curl" at the [eurorust](https://eurorust.eu) conference on
Thursday. It was a in-person conference in Berlin but I did my talk
remotely. Got a lot of attention and several good questions from an interested
audience.

## tiny-curl

I know, I said last week I would do a tiny-curl release this week but it did
not happen. I haven't forgotten, I just felt I had to prioritize other
things. Maybe it will be delayed another week.

## Blog posts

- [There is a tab in my cookie](https://daniel.haxx.se/blog/2022/10/14/there-is-a-tab-in-my-cookie/)
- [Rewriting curl in three days](https://daniel.haxx.se/blog/2022/10/14/rewriting-curl-in-three-days/)

## Coming up

- "The fund" deal is about to get signed and I hope to announce details soon
  about three exciting curl projects we will work on for the coming six
  months. Stay tuned.
  
- I will be doing two in-person talks i Östersund, Sweden, next week.

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# October 7, 2022

## security

The curl security audit is now in it's last week. I have been working fiercely
on addressing issues found and reported by **Trail of Bits**. They have
reported a slew of issues and frictions that have no real security impact but
still are good to fix, and those are being dealt with as normal pull-requests
on GitHub. A whole series of them in fact.

So far, they have reported one problem with an obvious security impact and we
are treating that as a vulnerability and it will result in a CVE to be
announced in sync with the pending next release.

Their CVE is in fact the *third* one queued up to be announced on October 26.
I have spent a lot of time this week working on all three to make sure we have
advisories, good patches and that the fixes include test cases that can both
reproduce the flaws and verify the fixes.

## white space

Followers of my activity and curl remember that we recently struggled with
HTTP/2 and how to deal with trailing white space in headers, as the recently
published RFC 9113 says we **MUST NOT** accept them but if we are that strict
it breaks a lot of things so nobody is. I even filed it as a possible [topic
to discuss at the HTTP
workshop](https://github.com/HTTPWorkshop/discussions/discussions/9) in
November.

This week in white space I took on an issue we got reported, dealing with TAB
characters within cookie names or in cookie contents. Since curl saves cookies
in a Netscape cookie file which uses tabs to separate fields, saving such
cookies would generate a broken cookie file.

RFC 6265 seems to allow tabs in there, but after checking what browsers do, I
learned that neither Chrome nor Firefox currently accept tabs in cookie names.
Chrome also rejects cookies with tabs in their values while Firefox strips off
the tabs from there(!).

I was prepared to [make curl reject such
cookies](https://github.com/curl/curl/pull/9659) as well, to follow the
pattern, but after [I brought up the
issue](https://github.com/httpwg/http-extensions/issues/2262) with the 6265bis
team (working on a cookie spec update), I was informed that the browsers are
actually now going in the other direction and will soon support tabs in cookie
names and values! This after [an
update](https://github.com/httpwg/http-extensions/pull/1589) to the 6265bis
document done last year... Apparently Safari already does. I can't easily
check, but I have no reason to doubt this.

Annoyed by this sick-sacking I proposed a second, alternative, curl change to
[encode TABS in the cookie jar
file](https://github.com/curl/curl/pull/9662). Right now it feels like this is
the more likely outcome for the curl camp. I think I will just let them hang
for a moment first and see if anything happens the 6265bis discussion that
changes things. Usually my objections are very light against the browser
people's though so I don't expect anything to change in a meaningful way.

## WebSocket

I took the next step in the WebSocket journey for curl this week. I [changed
the API slightly](https://github.com/curl/curl/pull/9636) in an attempt to
make it more usable, as I was informed that it really needs to support large
fragments.

We *can* change the API because this feature is still marked **experimental**
and for such features we do not guarantee stability or compatibility. Thanks
to this, we can keep develop it and not carve the API into stone until we
think the time is ripe and the design is "complete".

I am still interested in feedback and comments from people with actual
WebSocket use cases on how the API works or perhaps even more if there are any
problems with it!

## talk

I had the pleasure of physically visiting a Stockholm based company and did a
"lunch presentation" about curl - start, growth, how and that there might be
even more curl in the future etc. Lots of thoughtful questions, good food and
an interesting conversation with like-minded humans. Yeah, it actually is good
to get out and around every now and then.

## Blog posts

None this week.

## Coming up

- I'll talk about curl and rust on [EuroRust](https://eurorust.eu/) on Thursday
- the final report on the curl audit
- create examples and test code using/verifying the WebSocket API
- prepare for a tiny-curl release on latest curl

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

[here](all.md)
