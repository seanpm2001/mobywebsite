---
title: Moby Builder Report 2017-05-08
layout: post
author: Moby Dev Team
author-url: https://github.com/moby/moby/blob/4f3c5b2568c28a4e0fd1b69ec6f2e0a0715d8cf5/reports/builder/2017-05-08.md
excerpt_separator: <!--more-->
---

## Quality: Dependency interface switch

Proposal for [switching the dependency interface](https://github.com/moby/moby/issues/32904) for current builder package. That should fix the current problems with data leakage and conflicts caused by daemon state cleanup scripts.<!--more-->

Merged as part of this effort:

- [Move dispatch state to a new struct](https://github.com/moby/moby/pull/32952)
- [Cleanup unnecessary mutate then revert of b.runConfig](https://github.com/moby/moby/pull/32773)

In review:
- [Refactor builder probe cache and container backend](https://github.com/moby/moby/pull/33061)
- [Expose GetImage interface for builder](https://github.com/moby/moby/pull/33054)

### Merged: docker build --iidfile

[`docker build --iidfile` to capture the ID of the build result](https://github.com/moby/moby/pull/32406). New option can be used by the CLI applications to get back the image ID of build result. API users can use the `Aux` messages in progress stream to also get the IDs for intermediate build stages, for example to share them for build cache.

### New feature: Long running session

PR for [adding long-running session between daemon and cli](https://github.com/moby/moby/pull/32677) that enables advanced features like incremental context send, build credentials from the client, ssh forwarding etc.

@simonferquel proposed a [grpc-only version of that interface](https://github.com/moby/moby/pull/33047) that should simplify the setup needed for describing new features for the session. Looking for design reviews.

The feature also needs to be reworked after CLI split.

### buildkit

Not much progress [apart from some design discussion](https://github.com/moby/moby/issues/32925). Next step would be to open up a repo.

### Proposals for new Dockerfile features that need design feedback:

[Add IMPORT/EXPORT commands to Dockerfile](https://github.com/moby/moby/issues/32100)

[Add `DOCKEROS/DOCKERARCH` default ARG to Dockerfile](https://github.com/moby/moby/issues/32487)

[Add support for `RUN --mount`](https://github.com/moby/moby/issues/32507)

[DAG image builder](https://github.com/moby/moby/issues/32550)

[Option to export the hash of the build context](https://github.com/moby/moby/issues/32963) (new)

[Allow --cache-from=*](https://github.com/moby/moby/issues/33002#issuecomment-299041162) (new)

If you are interested in implementing any of them, leave a comment on the specific issues.

### Other new builder features currently in code-review:

[Allow builds from any git remote ref](https://github.com/moby/moby/pull/32502)

[Fix a case where using FROM scratch as NAME would fail](https://github.com/moby/moby/pull/32997)

### Backlog:

[Build secrets](https://github.com/moby/moby/pull/30637) will be brought up again in next maintainer's meeting to evaluate how to move on with this, if any other proposals have changed the objective and if we should wait for swarm secrets to be available first.
