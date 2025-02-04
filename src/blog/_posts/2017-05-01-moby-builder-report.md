---
title: Moby Builder Report 2017-05-01
layout: post
author: Moby Dev Team
author-url: https://github.com/moby/moby/blob/4f3c5b2568c28a4e0fd1b69ec6f2e0a0715d8cf5/reports/builder/2017-05-01.md
excerpt_separator: <!--more-->
---

## buildkit

As part of the goals of [Moby](https://github.com/moby/moby#transitioning-to-moby) to split the current platform into reusable components and to provide a future vision for the builder component new [buildkit proposal](https://github.com/moby/moby/issues/32925) was opened with early design draft.<!--more-->


Buildkit is a library providing the core essentials of running a build process using isolated sandboxed commands. It is designed for extensibility and customization. Buildkit supports multiple build declaration formats(frontends) and multiple ways for outputting build results(not just docker images). It doesn't make decisions for a specific worker, snapshot or exporter implementations.

It is designed to help find the most efficient way to process build tasks and intelligently cache them for repeated invocations. 

### Quality: Dependency interface switch

To improve quality and performance, a new [proposal was made for switching the dependency interface](https://github.com/moby/moby/issues/32904) for current builder package. That should fix the current problems with data leakage and conflicts caused by daemon state cleanup scripts.

@dnephin is in progress of refactoring current builder code to logical areas as a preparation work for updating this interface.

Merged as part of this effort:

- [Refactor Dockerfile.parser and directive](https://github.com/moby/moby/pull/32580)
- [Refactor builder dispatch state](https://github.com/moby/moby/pull/32600)
- [Use a bytes.Buffer for shell_words string concat](https://github.com/moby/moby/pull/32601)
- [Refactor `Builder.commit()`](https://github.com/moby/moby/pull/32772)
- [Remove b.escapeToken, create ShellLex](https://github.com/moby/moby/pull/32858)

### New feature: Long running session

PR for [adding long-running session between daemon and cli](https://github.com/moby/moby/pull/32677) that enabled advanced features like incremental context send, build credentials from the client, ssh forwarding etc. is looking for initial design review. It is currently open if features implemented on top of it would use a specific transport implementation on the wire or a generic interface(current implementation). @tonistiigi is working on adding persistent cache capabilities that are currently missing from that PR. It also needs to be figured out how the [cli split](https://github.com/moby/moby/pull/32694) will affect features like this. 

### Proposals for new Dockerfile features that need design feedback:

[Add IMPORT/EXPORT commands to Dockerfile](https://github.com/moby/moby/issues/32100)

[Add `DOCKEROS/DOCKERARCH` default ARG to Dockerfile](https://github.com/moby/moby/issues/32487)

[Add support for `RUN --mount`](https://github.com/moby/moby/issues/32507)

These proposals have gotten mostly positive feedback for now. We will leave them open for a couple of more weeks and then decide what actions to take in a maintainers meeting. Also, if you are interested in implementing any of them, leave a comment on the specific issues.

### Other new builder features currently in code-review:

[`docker build --iidfile` to capture the ID of the build result](https://github.com/moby/moby/pull/32406) 

[Allow builds from any git remote ref](https://github.com/moby/moby/pull/32502)

### Backlog:

[Build secrets](https://github.com/moby/moby/pull/30637) will be brought up again in next maintainer's meeting to evaluate how to move on with this, if any other proposals have changed the objective and if we should wait for swarm secrets to be available first.