# Daniel's weekly report

# December 10, 2021

## Happened this week

- Bonus points this week goes to Brad who toyed with running a server on TCP
  port zero and discovered that curl didn't support connecting to it! Extra
  embarrassing for me since I wrote blog post about exactly that feature years
  ago: [Pretending port zero is a normal
  one](https://daniel.haxx.se/blog/2014/10/25/pretending-port-zero-is-a-normal-one/)
  so obviously this was a regression! Luckily, the fix was very easy and
  order will be restored in the next curl release!
  
- I expanded [everything curl](https://everything.curl.dev/) with several
  hundred lines of new content and I worked on splitting up some of the
  largest pages into many smaller ones. All in an effort to make it easier to
  read and make better "landing pages" for different topics. Right now, I'm
  down to just 12 sections left marked "TBD" and a total of more 77,600 words
  written, using 667 section titles in 214 separate markdown files. I also
  passed 1,000 commits in the [git
  repo](https://github.com/bagder/everything-curl) this week. Don't forget to
  let me know when you find curl concepts not currently covered in the book!
  
- I managed to get 6 more test cases work with a hyper-powered build, now down
  to **26 disabled tests** to go. There are still more work for me to fix in
  there and we also need hyper to offer new APIs for some of them, most
  notably support for trailers.
  
- This week's hardest bug-fix was probably [multi: cleanup the socket hash
  when destroying it](https://github.com/curl/curl/pull/8131). Another win for
  "torture testing" (making resource allocating functions fail on purpose) but
  for some reason I could only ever reproduce the fail on mac and it took me a
  few hours to get to the bottom of it and make a clean fix.
  
- The possibly most unexpected side-effect of me spending a few hours staring
  at curl code using hash tables, was me converting the internal hash API to
  [lazy-initializing parts of it](https://github.com/curl/curl/pull/8132). Not
  only is the patch a negative line delta, it also removes a few allocs from
  my plain "malloc counter" test. Downloading a huge static file over HTTP now
  uses 91 allocations compared to 94 before. (The exact count will of course
  depend on build conditions; YMMV).

- The curl feature freeze went in effect this Wednesday. See also our [release
  cycle
  explained](https://curl.se/dev/release-procedure.html#release-cycle). The
  pending release is due on January 5, 2022. You can always find the pending
  RELEASE-NOTES for the coming version here:
  [https://curl.se/dev/release-notes.html](https://curl.se/dev/release-notes.html).

## Blog posts

- [No easter eggs in
  curl](https://daniel.haxx.se/blog/2021/12/06/no-easter-eggs-in-curl/). 150+
  comments on [hacker news](https://news.ycombinator.com/item?id=29460313),
  50+ on
  [reddit](https://www.reddit.com/r/programming/comments/racp85/there_are_no_easter_eggs_in_curl/) and 40+ on [lobste.rs](https://lobste.rs/s/ihmauf/no_easter_eggs_curl).

## Coming up

- fix more tests to work with hyper
- I'm participating in a panel discussion titled [The Future of Open Source:
  Is It
  Sustainable?](https://sentry.io/resources/the-future-of-open-source-is-it-sustainable/?utm_medium=partner&utm_source=curl&utm_campaign=event-open-source-2021)
  on Tuesday the 14th of December. Sign up to attend this free event organized
  by **Sentry**.

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# December 3, 2021

## Happened this week

 I started off the week with a bang. The primary server I take care of (owned
 and run by [Haxx](https://haxx.se)), which hosts the curl website origin,
 many mailing lists and a range of other services needed an upgrade. It runs
 Debian and we took the plunge and upgraded it to Debian 11. Just like that,
 on a Monday.
 
 This lax attitude of mine to a system upgrade, of course immediately hit me
 in the face when it dawned upon me that in **Debian 11** they no longer ship
 Python 2 and as direct side-effect of this: *mailman 2 is no longer provided*
 as a package, I believe because it is still only supported with Python 2. Our
 mailing list server on [lists.haxx.se](https://lists.haxx.se) run sixteen
 public mailing lists and a few private ones, and in this single careless
 upgrade they were all suddenly out of order.
 
 Debian 11 instead provides mailman 3. This is not just a typical upgrade from
 version 2 but is rather a fairly big and different take on mailing lists.
 Documentation might even make you believe that you can more or less
 automatically convert from a mailman 2 instance to a mailman 3 instance so I
 figured that is what I needed to do as well to stay with the times. I
 subsequently installed mailman3 and started configuring the machine to
 instead offer the lists to the world using this version, ran conversion
 scripts, modified server configs and configured the new services. I struggled
 with this during the rest of the Monday until late in the evening. By
 midnight I stopped and went to bed.
 
 Very annoyed over my troubles and over a (django) web server that runs and
 logs an error by dumping an entire python stack trace in the log file saying
 "can't find the database" but leaving out the only really interesting and
 important tidbit in that error: the file name of the database, I spent
 Tuesday on casually trying more things to get mailman3 up while other work
 needed some attention and I started to reconsider my options and how I should
 proceed to get the lists back up.
 
 Late Tuesday afternoon I decided to backpedal to at least get something up
 and working again sooner rather than later and the mailman3 config really
 made me lose my temper I felt as if I was going nowhere with it. I instead
 built Python2, mailman2 and pip (for python2) etc from source.
 
 Wednesday morning I restored the mailman2 configs for the web-server, fixed
 postfix to again work with it and tweaked my docker configs to use the new
 paths on my machine, tested the new config a tittle and then... at
 **10:03:03** Wednesday morning I could **finally** [send a mail to the
 curl-library](https://curl.se/mail/lib-2021-12/0000.html) informing everyone
 about the 46 hour glitch we just experienced. The lists were back up. On
 mailman2. I learned something. I think.
 
 Sticking to mailman2 might not be a solid long-term solution but at least
 things are now working again and I have time and opportunity to consider my
 future options in a more relaxed and planned-ahead way.

- I was contacted by a potential customer asking about the feasability of
  porting libcurl to offer FTP and SFTP powers on 16 bit CPU with 16K RAM...
  libcurl is not currently ported to 16 bit, and getting a general purpose FTP
  client into 16K is probably hard. Getting SFTP into the mix as well I deem
  is completely impossible.

- Found myself listed as the [5th most followed GitHub user in
  Sweden](https://github.com/gayanvoice/top-github-users/blob/main/markdown/followers/sweden.md)

- Talked open source supply chain security and sustainability with a
  journalist. How come something that is made by a small distributed team with
  very little funding can end up getting used by virtually everything and
  everyone?

- Attended the 2021 Polhem Prize award ceremony, [looking like
  this](https://twitter.com/bagder/status/1466430742813106188). Conversations
  with various (mostly engineers) at this event combined with the above
  mentioned discussion lies behind this week's blogpost of mine.

## Blog posts

- [Why curl is used everywhere, even on Mars](https://daniel.haxx.se/blog/2021/12/03/why-curl-is-used-everywhere-even-on-mars/)

## Coming up

- the curl feature freeze starts on Wednesday
- fix more tests to work with hyper

## Feedback

[Comment here](https://github.com/bagder/log/discussions)

# Older reports

- [November 2021](November-2021.md)
- [October 2021](October-2021.md)
- [September 2021](September-2021.md)
- [August 2021](August-2021.md)
