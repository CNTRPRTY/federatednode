Install Bitcoin + Counterparty with the following command:

`fednode install`

This installs a docker based manager for the minimal services required to have a Bitcoin + Counterparty node.

The main differences between this 'Core Version' setup vs. the "[official](https://counterparty.io/docs/federated_node/)" are:

- [Branched off](https://github.com/CNTRPRTY/federatednode/tree/counterpartyxcp_master) before the addition of non-required services to the 'base' configuration
- Also takes the opportunity to:
  - Defaults to CONFIG:base BRANCH:master
  - Makes the `--no-bootstrap` option default (Don't trust, verify)
  - Installs v0.21.0 of Bitcoin Core (but [easy](https://github.com/CNTRPRTY/federatednode/blob/master/extras/docker/bitcoin/Dockerfile#L27) to change to your preferred version)
  - Security improvements
  - (see [commits](https://github.com/CNTRPRTY/federatednode/commits/master), verify)

This fednode software is used by [xcp.dev](https://www.xcp.dev/) ([DIY](https://github.com/CNTRPRTY/xcpdev/tree/main/server/fednode)).

---

[![Slack Status](http://slack.counterparty.io/badge.svg)](http://slack.counterparty.io)

**All-in-one Counterparty Federated Node Build System (`federatednode`)**

Allows one to easily build a counterparty-server with all required components. Uses Docker and Docker compose.
<!-- Allows one to easily build a counterparty-server, `counterblock` and/or Counterwallet system, with all required components. Uses Docker and Docker compose. -->

See documentation at <http://counterparty.io/docs/federated_node/>.

Please issue any/all pull requests against **develop**, not **master**.
