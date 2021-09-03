# Daniel's weekly report September 3, 2021

## Happened this week:

 - Did more work on hyper. Now at 64 disabled tests remaining to
   fix. Primarily I fixed how libcurl does Transfer-Encoding in the presence
   of Content-Length headers, as it was previously done wrongly. I then got a
   little stuck on NTLM with CONNECT to a proxy but I've figured out roughly
   what's wrong and that needs to be done. It's just a little complicated.

 - Moved a lot of mailing lists from cool.haxx.se to lists.haxx.se as a step
   in the shutting down of the old dying server. The libssh2 website is the
   last one to get transitioned and it is now in progress.

 - Extended the curl man page with examples - for every single command line
   option - and I'm working on polishing up examples and more in the libcurl
   option man pages.

 - Got an idea for curl's 25th birthday: curl v8:
   https://curl.se/mail/lib-2021-09/0009.html

 - My talk at netnod tech meeting on October 13 was announced:
   https://www.netnod.se/netnod-events/netnod-tech-meeeting-2021-1/agenda

## Blog posts:

 - working on a (curl) docs post
 - working on a post-quantum curl post

## Coming up:

 - More hyper work to do.

