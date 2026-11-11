# Privacy Guide in 2025

## Privacy Guide in 2025

> My personal privacy setup and recommendations. The email alias section pairs with the step-by-step General/Privacy/SimpleLogin - HowTo.

I'll start by saying this again: privacy is what **YOU** want it to be. There are a lot of ways to go about it; some are more simple while others are more in-depth and require more effort. If you want to use social media that targets you with ads and tracks and listens to you, but you are aware of that, then by all means! But you have control over how much of your data they get and the ways they track you. Privacy can be a rabbit hole, but take it as far as you want - not what others may tell you is or isn't enough.

While some of this might be at the slight cost of convenience, it ends up being better for you overall in most cases. Keep in mind that **privacy ≠ anonymity**.

Anonymity is about keeping yourself unidentified or unidentifiable. The important idea about anonymity is that a person be non-identifiable, unreachable, or untraceable.

Privacy, on the other hand, is about it not being important if they know who you are, but hiding what you are doing. In my case, it's about hiding it from big tech. My data is for sale as much as anyone else's; I'm just making sure as little of it as possible is out there for sale. If the product is free, there's a high chance that you are what they are selling to others.

There's a good article breaking down the difference between the two [here](https://proton.me/blog/anonymity-vs-privacy) by [Douglas Crawford](https://proton.me/blog/author/dcrawford) at Proton.

Most of these tools are free or have very small price points. The hardware will come down to your personal phone and/or computer. Also, don't forget to Google yourself from time to time - and if there's anything your name is on that you want removed, you can start that process.

## Emails

I use the [Proton Suite](https://proton.me/), but there are other alternatives such as [Tutanota mail](https://tutanota.com/). Some advise against this due to "not having all your eggs in one basket," but in my opinion it's still perfectly acceptable, as long as your security is spread around.

I personally like and prefer Proton as they go for privacy as the basis of all of their products. They are a bit slower to release/update things for Linux and iOS, but they do get released. Proton is free, with options to upgrade to paid plans for more storage, custom domains, additional emails, etc.

## Email Alias

Next would be to log in to [SimpleLogin](https://simplelogin.io/) with your Proton account, or you can make your own account without using Proton. You'll use this to create emails for individual accounts/services you'll be using and making. An alternative is [AnonAddy](https://anonaddy.com/).

This is insanely helpful when signing up for services or websites, as the email alias created will forward everything to your real email. So in the event of a data breach, they don't get your real email address. You can also disable the alias temporarily and turn it back on whenever you want, so as not to get spam mail.

> For a full walkthrough of setting this up, see General/Privacy/SimpleLogin - HowTo.

## VPN

There are really two options: [ProtonVPN](https://protonvpn.com/) and [Mullvad VPN](https://mullvad.net/). I use ProtonVPN due to having an active subscription, so I get the premium included. It does include a free tier for users as well.

## Payments

When making online payments, use [Privacy.com](https://privacy.com/). This lets you create virtual payment cards for one-time purchases or subscriptions. **NOTE:** Some services will not let you, or will fight you on, using these virtual cards.

## Browsers

[Firefox](https://firefox.com/) - I myself am a fan of [Hardened Firefox](https://www.privacyguides.org/en/desktop-browsers/#firefox) (and [this guide](https://brainfucksec.github.io/firefox-hardening-guide) by [brainfucksec](https://brainfucksec.github.io/whoami)), due to the ability to have [Containers](https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/). "Each container is isolated from the others, so you can access sites logged into different accounts." This keeps sites isolated from each other so as not to share cookies and other info.

[LibreWolf](https://librewolf.net/) - a fork of Firefox that has most of the "hardening" or privacy settings on by default, but it's a little slower to be updated than normal Firefox. As a fork of Firefox, it has the ability to use containers the same way Firefox does.

[Brave](https://brave.com/) - a Chromium-based browser that has other privacy and ad-blocking features built in out of the box. You can let it show you ads and it will pay you a minor amount as you browse, but keep in mind that it does also collect some of your data as you browse.

Additionally, use [uBlock Origin](https://github.com/gorhill/uBlock#ublock-origin) with any browser you do use.

### Searching

Rather than use Google, you can use something like [DuckDuckGo](https://duckduckgo.com/) or [StartPage](https://www.startpage.com/). I recommend StartPage.

## Password Managers

There are a few out there. There isn't an exact wrong answer, but some have a poor reputation from being breached. I myself use [Bitwarden](https://bitwarden.com/). This is free, and if you want to pay to self-host (recommended) and get other features, it's only $10 a year. Super cheap and worth it. Alternatives are [Proton Pass](https://proton.me/pass) or [1Password](https://1password.com/).

## Keeping In Contact / Messaging

This is a pain point for a lot of people, as most don't want _another_ app to message someone, or to switch off of their current one. So many people use one or two platforms already that either adding one more or trying to convince someone to switch isn't always easy.

[Signal](https://signal.org/en/) - a great one, minus the caveat that you need a phone number to sign up. They have [Signal Usernames](https://www.signal.org/blog/phone-number-privacy-usernames/), so you don't need to give people your phone number anymore. Great to use as they also have a desktop app, capable of sending files, audio messages, and video calls. I use Signal the most, though I will be trying to switch to [SimpleX](https://simplex.chat/).

[SimpleX](https://simplex.chat/) - also a great one, as it doesn't require a phone number to sign up. You generate a link or a QR code to share, and people find you that way. Also great as they have a desktop app, capable of sending files, audio messages, and video calls.

[Element](https://element.io/) - a way to chat using [Matrix](https://element.io/matrix-benefits). This can be used for individuals or for creating chatrooms. It has the ability to search for open/public chatrooms, or create your own. This one replaces Discord.

[MySudo](https://mysudo.com/) - for creating phone numbers, emails, etc. to use instead of your real personal information. **Note:** You _may_ need a stock Android or iPhone device to sign up for a plan. I had an older stock Android phone around, downloaded the app, signed up for the service, and logged into the account on my non-stock Android phone.

[Cryptomator](https://cryptomator.org/) - for use with any cloud storage that you don't sync. This will encrypt files that are put onto any online cloud storage.

## Cloud Storage

I use [Proton Drive](https://proton.me/drive), with some self-hosting using [NextCloud](https://nextcloud.com/). NextCloud is used if you have a home server or spare machine to set it up on. This is a way to keep important files backed up, or to share larger files with others. If you happen to store any sensitive data on cloud storage, I recommend encrypting it with [Cryptomator](https://cryptomator.org/) to increase security on those files/folders.

## Note Taking

Most note-taking apps have the ability to read your notes. Notes may not seem like a major thing, but some people take quick notes that have personal or sensitive information. I use [Obsidian](https://obsidian.md/) and have used [Joplin](https://joplinapp.org/) in the past. Both are great, but if you want to sync notes, you'll need to pay or have a cloud storage of some form to sync them. Both have a great amount of community plugins that enhance the apps.

## Calendar

I use Proton [Calendar](https://proton.me/calendar); this is primarily for me and my spouse to share together. I don't use calendars too much other than this, but I still want to keep my data private.

## 2FA/MFA

This should also be used everywhere, with any account that allows it. I recommend using [Aegis Authenticator](https://getaegis.app/). There are more secure ways, such as using a [YubiKey](https://www.yubico.com/) and its [authenticator](https://www.yubico.com/products/yubico-authenticator/) - this requires you to carry it with you for use at all times. Bitwarden also has one built into its password manager, but it's better to keep these separate so that if your Bitwarden somehow gets compromised, they won't have your 2FA/MFA codes.

## AI

If you're someone who uses AI for various things, I suggest using [Lumo](https://lumo.proton.me/). I personally don't use AI too much, but this is one that isn't logging or harvesting your chats/data. It may not be as advanced as others, but it is privacy-respecting.

## Hardware

### Mobile

I personally recommend a Google Pixel phone (unlocked) and installing [GrapheneOS](https://grapheneos.org/). iPhones are a good alternative over stock Android. Use [Mint Mobile](https://www.mintmobile.com/) instead of a normal carrier, so you'll be getting a new phone number. When giving out your new phone number to family/friends, make sure you trust them not to give it out to others.

### PC

Most machines work and will depend on your use case, but rather than using Windows or macOS, go with [Qubes OS](https://www.qubes-os.org/) (for more advanced users) or base [Debian Linux](https://www.debian.org/). I typically use Debian for ease, as most things just work with it and it works great for my day-to-day things.

If you use Windows 11 (as Windows 10 is soon to be unsupported), you'll want to take some extra steps like running [O\&O ShutUp10++](https://www.oo-software.com/en/shutup10) and [O\&O AppBuster](https://www.oo-software.com/en/ooappbuster). These remove unnecessary bloat apps and software, and disable/enable certain built-in Windows features that collect your data. You can use [Chris Titus's Windows Utility](https://github.com/ChrisTitusTech/winutil) for additional options.

## Conclusion

There are multiple options out there when it comes to your online privacy and security. Take it as far as you want. There's social media and services where you are the product they're selling, and plenty of others where you still are the product even if you're paying. I myself use social media in its own container on Firefox, but I don't have the apps installed on my phone - I just access them via my phone's browser if I want/need to. I use apps like Discord that collect your data because it's hard not to when a vast majority of people use it, but the ones who are privacy-conscious/respecting will use the other apps with me.
