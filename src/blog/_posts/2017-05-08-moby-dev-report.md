---
title: Moby Dev Report 2017-05-08
layout: post
author: Moby Dev Team
author-url: https://github.com/moby/moby/blob/4f3c5b2568c28a4e0fd1b69ec6f2e0a0715d8cf5/reports/2017-05-08.md
excerpt_separator: <!--more-->
---

## Daily Meeting

A daily meeting is hosted on [slack](https://dockercommunity.slack.com) every business day at 9am PST on the channel `#moby-project`.
During this meeting, we are talking about the [tasks](https://github.com/moby/moby/issues/32867) needed to be done for splitting moby and docker.<!--more-->

## Topics discussed last week

### The CLI split

The Docker CLI was succesfully moved to [https://github.com/docker/cli](https://github.com/docker/cli) last week thanks to @tiborvass
The Docker CLI is now compiled from the [Dockerfile](https://github.com/moby/moby/blob/a762ceace4e8c1c7ce4fb582789af9d8074be3e1/Dockerfile#L248)

### Mailing list

Discourse is available at [forums.mobyproject.org](https://forums.mobyproject.org/) thanks to @thaJeztah. mailing-list mode is enabled, so once you register there, you will received every new threads / messages via email. So far, 3 categories were created: Architecture, Meta & Support. The last step missing is to setup an email address to be able to start a new thread via email.

### Find a place for `/pkg`

Lots of discussion and progress made on this [topic](https://github.com/moby/moby/issues/32989) thanks to @dnephin. [Here is the list](https://gist.github.com/dnephin/35dc10f6b6b7017f058a71908b301d38) proposed to split/reorganize the pkgs.

### Find a good and non-confusing home for the remaining monolith

@cpuguy83 is leading the effort [here](https://github.com/moby/moby/pull/33022). It's still WIP but the way we are experimenting with is to reorganise directories within the moby/moby.

## Componentization

So far only work on the builder, by @tonistiigi, happened regarding the componentization effort.
