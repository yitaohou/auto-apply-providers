# job-searcher

Provider for `job.search@1`. Browses LinkedIn and Indeed with ego lite and appends
matching postings to your job queue.

## Before first use

1. Open ego lite and **log in to Indeed**. The provider reads Indeed's listings through
   your browser session and cannot log in for you.
2. LinkedIn needs no login — its job search is readable anonymously.

If Indeed is not logged in, searches that include it return an error rather than
partial results.

## Choosing sources

By default this provider searches **LinkedIn only**. To change that for a run, include
a `sources=` directive in `requirements` in `data/search_profile.csv`:

    sources=linkedin    LinkedIn only (default)
    sources=indeed      Indeed only
    sources=both        both sites

The value must be one of those three literals. Anything else is rejected rather than
guessed at.

## What it does not do

It never applies to a posting, saves it, or interacts with it in any way beyond reading
the listing. It never logs in or enters credentials. It appends to `queue.txt` and
reads one column of `job_pool.csv`; it touches no other file.

## Automated browsing and your accounts

This provider drives a real browser session against LinkedIn and Indeed. Automated
access may be against those sites' terms of use, and enforcement typically takes the
form of rate limiting or account restriction. Consider which account you are signed
into, especially on LinkedIn if you are actively job hunting there.
