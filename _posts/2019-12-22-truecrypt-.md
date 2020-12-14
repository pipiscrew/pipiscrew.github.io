---
title: TrueCrypt and German Secrets
author: PipisCrew
date: 2019-12-22
categories: [news]
toc: true
---

TrueCrypt is an amazing piece of software that literally changed the world, giving every computer user a free, source-available solution for hard drive encryption. While the source of the program was made freely available, the license was odd and restrictive enough that it’s technically neither Free Software, nor Open Source Software. This kept it from being included in many of the major OS distributions. Even at that, TrueCrypt has been used by many, and for many reasons, from the innocent to reprehensible. TrueCrypt was so popular, a crowdfunding campaign raised enough money to fund a professional audit of the TrueCrypt code in 2013.

The story takes an odd turn halfway through the source code audit. Just after the initial audit finished, and just before the in-depth phase II audit was begun, the TrueCrypt developers suddenly announced that they were ending development. The TrueCrypt website still shows the announcement: “WARNING: Using TrueCrypt is not secure as it may contain unfixed security issues.” Many users thought the timing was odd, and speculated that there was a backdoor of some sort that would be uncovered by the audit. The in-depth audit was finished, and while a few minor issues were discovered, nothing particularly serious was uncovered.

One of the more surprising users of TrueCrypt is the German government. It was recently discovered that the BSI, the information security branch of the German government, did an audit on TrueCrypt back in 2010.

Many governments have now have laws establishing the freedom of information, granting a “right-to-know” to their citizens. Under these laws, a citizen may make an official request for documentation, and if such documentation exists, the government is compelled to provide it, barring a few exceptions. A German citizen made an [official request](https://translate.google.com/translate?sl=auto&tl=en&u=https%3A%2F%2Ffragdenstaat.de%2Fanfrage%2Ftrue-crypt-unterlagen-und-backdoor%2F) for information regarding TrueCrypt, particularly in regards to known backdoors in the software. Surprisingly, such documentation did exist!

Had the German government secretly backdoored TrueCrypt? Were they part of a conspiracy? Probably not. After some red tape and legal wrangling, the text of the audit was finally released and cleared for publication. There were some issues found back in 2010 that were still present in the TrueCrypt/Veracrypt source, and got fixed as a result of this report coming to light.

https://hackaday.com/2019/12/20/this-week-in-security-unicode-truecrypt-and-npm-vulnerabilities/

ref - [https://www.pipiscrew.com/2019/12/new-evidence-suggests-satoshi-nakamoto-is-paul-solotshi-the-creator-of-encryption-software-e4m-and-truecrypt/](https://www.pipiscrew.com/2019/12/new-evidence-suggests-satoshi-nakamoto-is-paul-solotshi-the-creator-of-encryption-software-e4m-and-truecrypt/)

+ Google Cloud Shell

origin - https://www.pipiscrew.com/?p=16392 truecrypt-and-german-secrets