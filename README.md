# Daniel's weekly report

# May 13, 2022

## Happened this week

### release

After 14 intense days since the previous release I once again had to go
through the release dance and upload [another
curl](https://daniel.haxx.se/blog/2022/05/11/curl-7-83-1-it-burns/) package
with a new version. This time in association with **6** new security
vulnerabilities, which of course burned in my ego.

The interesting and probably hardest part about getting security
vulnerabilities reported in the project is to learn from them.

1. Why did they happen?
2. How come we did not find them sooner?
3. Can we find other similar mistakes in the existing code?
4. How are we going to make sure similar mistakes are not introduced in the
   future?

It is easy to see and say that clearly we did not have good enough tests, but
that is not helping.

I do not have many answers for you on these questions today, but I am certain
that I will continue to wrestle with them going forward. I am still convinced
that curl and libcurl are very secure products and I will continue to work
hard on improving the code all over. The iterative process never stops.

### trailing dots

The dreaded trailing dots in host names were involved in at least three curl
bugs fixed in the latest release, out which two ended up security problems. I
explain those at some depth in a [blog
post](https://daniel.haxx.se/blog/2022/05/12/a-tale-of-a-trailing-dot/)
dedicated to the subject.

### curl up

Google and GitHub are two additional sponsors of [curl up 2022](https://github.com/curl/curl-up/wiki/2022). We are slowly adding more content to the agenda. Feel most welcome to help us with this!

### curl.se hosting

I proposed we put an end to my over twenty years long period of paying for curl.se hosting and maintenance mostly out of my own pocket, and propose [the project compensates me](https://curl.se/mail/lib-2022-05/0017.html) with a fixed amount of money per year.

### past vulnerabilities

I spent some time this week digging into the history of eleven older curl
CVEs, all for which we had "7.1" set as *first vulnerable version*. In reality
none of them were introduced then and I had only set that very lazily back in
the day! Eight of them turned out older and three of them were newer and now
the info on the website shows this correctly. Nowadays when I write up
security advisories for curl, I always get to the bottom to exactly in which
commit and version vulnerabilities were introduced. It takes time, but I think
the service to the community makes it worth it.

I also recently updated the [security
problems](https://curl.se/docs/security.html) page on the curl website to be
more focused and narrower - by dropping the CWE name and the MITRE links from
the main table. I don't think they made much use there and now the table is
much easier on the eye.

## Blog posts

- [curl 7.83.1 it burns](https://daniel.haxx.se/blog/2022/05/11/curl-7-83-1-it-burns/)
- [A tale of a trailing dot](https://daniel.haxx.se/blog/2022/05/12/a-tale-of-a-trailing-dot/)

## Coming up

- The annual curl user survey!
- The curl feature window opens
- Two rather big customer requested new curl feature projects to discuss/kick
  off

## Feedback

[Comment here](https://github.com/bagder/log/discussions)


# May 6, 2022

## Happened this week

### Uncurled

[Announced](https://un.curl.dev)

### curl release

After the 7.83.0 release we received what can only be described as an
avalanche of security vulnerability reports. We immediately gave up the idea
of opening the feature window and instead readjusted our aim on doing a patch
release soon.

### Security

This week we have announced that the patch release will happen on May 11 and
that we have *at least* six new vulnerabilities to announce in association with
that release. This does not include the number of reports we worked on that we
dismissed as *not* security related, but there are a whole bunch of those as
well. Quite clearly several good and security oriented people decided to
scrutinize curl at the same time.

Analyzing, discussing, testing, debugging, documenting and patching these
issues have taken just about all my time since the previous release.

### curl up

The [agenda](https://github.com/curl/curl-up/wiki/2022) for June 6 is slowly
getting populated, but there are still several gaps we want to fill with
quality presentations. Let me know what subjects you can help out with!

We have two well-known sponsors lined up but not quite yet announced. Stay
tuned.

Thanks to sponsors, we will provide lunch.

### Daniel in the bay area

Tangentially related to curl up, but since I will fly over to San Francisco to
attend and present at curl up on June 6th, I will be in the general SF Bay
Area a few days following that event. I am in the process of nailing my
agenda, but if you want to arrange a meetup or something, do hit me up and
let's see what we can do. Might as well maximize my time there.

### WinCE

Customer XYZ got libcurl and wolfssl to build and run on WinCE 5.0 and after a
meeting with me Thursday, seem to be well on their way to get the combination
to work as well and thus targeted to meet their very tough deadline.

## Blog posts

- [Uncurled](https://daniel.haxx.se/blog/2022/04/30/uncurled/)
- [Considered “18+”](https://daniel.haxx.se/blog/2022/05/02/considered-18/)
- [now on HTTP/3](https://daniel.haxx.se/blog/2022/05/02/now-on-http-3/)
- [Meeting the Cyber Safety Review Board](https://daniel.haxx.se/blog/2022/05/05/meeting-the-cyber-safety-review-board/)

## Coming up

- WebSockets is happening?
- curl 7.83.1 on Wednesday
- webinar: Why everyone is using curl and you should too (on Thursday)

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older weekly reports

- [April 2022](April-2022.md)
- [March 2022](March-2022.md)
- [February 2022](February-2022.md)
- [January 2022](January-2022.md)
- [December 2021](December-2021.md)
- [November 2021](November-2021.md)
- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
