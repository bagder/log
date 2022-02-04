# Daniel's weekly report

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
