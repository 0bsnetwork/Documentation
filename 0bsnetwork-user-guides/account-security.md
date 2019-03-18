# Account / Wallet Security

## General

In the self-sovereign land of true public permissionless blockchain, account security is a crucially important topic. 
At the same time, it is fundamentally different from the "old ways" of bank accounts, cloud service accounts and any other centralised system we're used to dealing with. The main difference is who is actually in charge. On 0bsnetwork, it is you!

If you have an account with a bank, or on any centralised online service (email, social media, community website, property rental portal, car sharing service, etc), the entity with which your account is registered is in control of it. They may have a policy of not accessing your information, but if they want to, they can. That's obviously a bad thing, however the advantage of such approach is that if you ever lose access to your account, or inadvertently give it away to someone else (a hacker, for example, or a work colleague who watches over your shoulder as you're typing in your password), you can simply ask the service provider to reset your password, send you the login credentials, or your PIN code, again, and all is good.

That's the exact opposite of how a true public blockchain platform works with user accounts. On 0bsnetwork, you control your account (also referred to wallet, address...) using your private key. And your private key is uniquely represented by the 15-word Seed Phrase. Each Seed Phrase "opens", controls and is tied to one account and there is absolutely no way to reset it, or recover it if lost.

Seed Phrase is case sensitive! "atom client fault" is not the same as "atom Client fault". More importantly, it is also not the same as "atom client  fault" (this has one extra space), nor as "atom client fault." (period at the end), nor is it necessarily the same as "atom client fault". This last version of an incorrect Seed Phrase is the most difficult to recognize, as it looks the same, but therefore also probably most important to pay attention to. Namely, various text editors on Windows or other operating systems can sometimes introduce hidden characters into a sentence. Sometimes there is a "new line" character at the end. So if you are trying to recover an account from a seed phrase you've copied from somewhere and it doesn't work, try typing it in manually, letter by letter.

**Back up your Seed Phrase!** Store it securely, so that noone can access it but you, and in several locations, so that if one is lost (due to fire, for example), you can retrieve another. Think about business continuity as well. What happens if you're hit by a tram next week? How will your family, or business associates be able to recover your account?

If you inadvertently give access to your Seed Phrase to anyone else, the only thing you can do, if you act quickly (!), is to transfer all the funds from that account to a new one. If you fail to do so, whoever has access to your account is very likely to transfer your funds to another account that they control. A different type of a problem arises if you used this account to create your own token, or deploy some important smart contracts. In such cases, we'd recommend that you urgently create a multi-signature setup with at least two new accounts that you create, so that your original account is useless without co-signature from at least one of the newly created ones. That way the "attacker" won't be able to do anything with the account, and you will retain control.

In both of these cases (loss of seed phrase, or another person gaining access without you acting quickly to avert disaster), your funds are irretrievably gone!

If you're storing larger amounts of ZBS Coins, or other tokens created on 0bsnetwork platform, it's a good idea to divide your funds across several accounts. 


## Using the Client and/or 0bsLink

The official 0bsnetwork end user software is our Client, available at [https://client.0bsnetwork.com](https://client.0bsnetwork.com), and we're also making available a web browser extension 0bsLink, which is used for interactions between any web applications and the 0bsnetwork blockchain. 
When accessing the Client, make sure (!) that your browser is showing the address mentioned here, together with a green "lock" symbol, to be certain that you're visiting the official Client and the connection is securely encrypted. It is possible and likely that some hacker somewhere will atempt to collect users' Seed Phrases by making a website that looks exactly like our official Client and asking you to import your account from the Seed Phrase for some reason that might seem legitimate. Don't fall for it and always pay close attention to what you're doing and where.

At the time of account creation, or when you restore your existing account by entering your Seed Phrase on a new device, you have the option to store that account locally, give it a name and protect it with a password. **This name and password combination is only valid on that one device where you created it.** It is not stored on any server and you cannot recover your 0bsnetwork account by entering that name and password on another device. 

When you use the official 0bsnetwork Client, your private key never leaves your device (PC, tablet, smartphone) that you're using to access the Client. All of the transactions that you initiate are signed using your private key on the device, locally, and the signed transaction is then broadcast to the blockchain platform. So, since your private key never leaves your device, there is no way for it to be stolen "in transfer". However, it can be stolen from your device, by any programs, malware, key loggers etc., that can read the contents of your creen, or of the websites you visit. Therefore, make sure that your PC is virus-free. Also, make sure noone is viewing or recording your screen while entering the seed phrase.

We're also making available the 0bsLink browser extension, for "blockchainisation" of web apps. Using 0bsLink, you can safely and securely interact with any compatible website. Sign transactions, sign documents, ... All of the signing is done locally, as with the Client, so your private key never leaves your device. Same words of caution about safekeeping your Seed Phrase apply here as well.


## Be Paranoid!

Accessing the Client or using 0bsLink from your regular devices that you use for work, school or fun every day is easy, convenient and great if you're certain that your device (PC, tablet, smartphone) is free from malware and 100% under your control, or if you're using that device to access an account with a limited amount of coins and tokens, that you could live without even if they god lost.

For storing (very) large amounts of coins and tokens, or for controlling an account which you used to create business-critical tokens, it would be prudent to always use a fresh device, which has never been exposed to the Internet before and which definitely doesn't have any compromised software installed. That would get pretty expensive pretty soon, if there weren't Live Linux distributions, such as [Tails](https://tails.boum.org/). Using Tails, or another Live Linux distribution, you're starting your PC from a freshly installed operating system, with no software that was added after the installation whatsoever. The downside is that you'll have to restore your account from the Seed Phrase every single time you want to use it. So the security of your Seed Phrase backup becomes even more important.

The download, installation and usage instructions for Tails Linux is beyond the scope of this article, but it's all pretty straightforward and well described at the Tails website.


## Be Very Paranoid!

The most secure way to use 0bsnetwork accounts is to never ever have your private key stored on or acceessed from a device which connects to the Internet at all. There are two possibilities: hardware wallets, such as Trezor or Ledger (support for both is on our roadmap and is coming soon), or a dedicated offline PC.

In order to use a dedicated offline PC, you'll need to get your hands a bit more dirty with command line commands, scripts and such. We'll write up some user manuals as soon as we physically can, but for now we just want to point you in the direction of 0bsPy - a Python library and set of scripts for offline transaction signing. You can [start investigating here](https://github.com/0bsnetwork/ZbsPy). 


Stay safe and have fun with 0bsnetwork :: Blockchain For The Real World!
