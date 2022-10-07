# Daniel's weekly report

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
