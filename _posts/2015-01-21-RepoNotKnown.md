---
layout: post
title: Repository not known to Travis
---

So I had a recent roadbump in how I was deploying this blog. After a moderate amount of googling, I was unable to find anything relating to the issue. (Maybe my googling skills are simply underdeveloped...)

So I thought it helpful to leave my (amateurish) findings here, so that others may google the issue with more productive results.

So a quick run down of how this site was made and deployed:

* Basic [Jekyll](http://jekyllrb.com) static site.
* [Hyde](https://github.com/mdo/hyde) for the theme.
* Source hosted on [Github](https://github.com), with the following webhook:
* [Travis-CI](https://travis-ci.org). Continuous integration is cool!
* Scripted .travis.yml file will build the Jekyll site and deploy!
* Deploys to AWS S3 bucket(s).

I'll need to revisit and document the whole process so I can relearn what was done. It was too valuable a learning process to simply forget exactly what was done. I'm mostly interested in the DNS naming/routing part, as I was basically just walked through it. There are simply too many ways to host a website to not get a handle on at least one and be able to use it in the future.

So, on to the issue I was having.

> $ travis encrypt --add xxxxxxxxxxxxxxxxxxxxxxxxx
> $ repository not known to https://api.travis-ci.com/:repoOwner/repoName

I was trying to encrypt an AWS key to allow travis-ci to deploy on its own. This was working fine some time ago...weird.

So what I tried:

* Read up on the [docs](http://docs.travis-ci.com/user/deployment/s3/) for S3 deployments a little more closely.
* Disable/reenable github webhook to travis-ci
* Try various travis commands from the terminal. Each gave the same error.
* Google more.

I shot off an email to travis-ci support and shelved my curiousity for a short while. What I got in response made me question my overall intelligence:

* You may have to explicitly hit the api.travis-ci.org endpoint, either via `--org` or `-e https://api.travis-ci.org'

travis-ci.com is for private repos and costs monthly.
travis-ci.org is for open source/public repos and is free.

The error I got back told me very blatantly it was trying to find my repo in the commercial version. Several times. Maybe that's why there wasn't very many relevant google results.

Besides the (now) very obvious mixup, was how this happened in the first place. The .git/config file had nothing about which site was referenced, and at one point, the site was being built and deployed fine. Then, after an absent-minded git push or two, I noticed the .travis.yml file was simply missing...

Computer ghosts. Or user ignorance.

Hope this helps someone and I'm not sharing my embarrassing amateurism for nothing.
