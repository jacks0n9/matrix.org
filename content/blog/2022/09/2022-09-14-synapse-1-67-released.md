+++
title = "Synapse 1.67 released"
date = "2022-09-14T13:03:21Z"
path = "/blog/2022/09/14/synapse-1-67-released"

[taxonomies]
author = ["Brendan Abolivier"]
category = ["Releases"]
+++

It's that time again - Synapse release time! [Synapse
1.67](https://github.com/matrix-org/synapse/releases/tag/v1.67.0) is fresh out
of the oven, let's have a look at what's inside.

<!-- more -->

## Removal of TCP replication

As announced in the [Synapse 1.66 release
announcement](https://matrix.org/blog/2022/09/02/synapse-1-66-released), Synapse 1.67 removes support for the legacy TCP replication protocol.

As a reminder, Synapse can be configured to use workers to spread its load over
multiple processes, or even multiple machines. These workers communicate between
each other (and with the main Synapse process) using something we call
"replication".

[Synapse 1.18](https://github.com/matrix-org/synapse/releases/tag/v1.18.0)
deprecated its TCP-based replication protocol, and replaced it with a brand new
one using [Redis](https://redis.io/). As of Synapse 1.67, this Redis-based
protocol is now the only protocol that can be used.

See the [upgrade
notes](https://matrix-org.github.io/synapse/v1.67/upgrade.html#direct-tcp-replication-is-no-longer-supported-migrate-to-redis)
for more information.

## Changes for installations using a source checkout

Server admins who installed Synapse using a source checkout might already be
familiar with [Poetry](https://python-poetry.org/). This is a tool we use
to better manage dependencies within Synapse. As of this version, we have
updated Synapse's dependency on Poetry to require Poetry 1.2, which was recently
released.

It is also worth noting that Synapse 1.68, which is due to release on the 27th
of September, will require a Rust compiler when installed from a source
checkout. This is because we are in the process of introducing Rust in Synapse's
code base, in order to make some hot code paths more efficient. See the [upgrade
notes](https://matrix-org.github.io/synapse/v1.67/upgrade.html#rust-requirement-in-the-next-release)
for more information.

These two changes should not impact installations that use `pip install
matrix-synapse`, Debian packages from `packages.matrix.org` or the
`matrixdotorg/synapse` Docker image to manage and run Synapse.

## Everything else

Synapse 1.68 (due on the 27th of September) will also require SQLite v3.27.0 or
higher when run with SQLite. Synapse 1.67 is the last version of Synapse to
support SQLite versions 3.22 to 3.26. See the [upgrade
notes](https://matrix-org.github.io/synapse/v1.67/upgrade.html#sqlite-version-requirement-in-the-next-release)
for more information.

See the [full
changelog](https://github.com/matrix-org/synapse/releases/tag/v1.67.0) for a
complete list of changes in this release. Also please have a look at the
[upgrade
notes](https://matrix-org.github.io/synapse/v1.67/upgrade#upgrading-to-v1670)
for this version.

Synapse is a Free and Open Source Software project, and we'd like to extend our
thanks to everyone who contributed to this release, including (in no particular
order) [Dirk Klimpel](https://github.com/dklimpel),
[Beeper](https://www.beeper.com/) and [Jacek
Kuśnierz](https://github.com/Vetchu), as well as anyone helping us make Synapse
better by sharing their feedback and reporting issues.
