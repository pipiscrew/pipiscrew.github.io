---
title: Bitlocker or TrueCrypt is safe?
author: PipisCrew
date: 2017-11-20
categories: [news]
toc: true
---

According to the [Passware Kit Forensic](https://www.passware.com) company, any computer that has **hibernated** even once with a mounted **TrueCrypt** or **BitLocker** hard drive is vulnerable, as their product can "instantly decrypt the hard disk even if the computer is no longer running".

ZoneAlarm DataLock (discontinued 2012), a third-party whole-disk encryption product, during the initial encryption stage disables hibernation. Afterward it interacts with the hibernation feature so that the encryption password is required on waking from hibernation.

If you do use **BitLocker** or **TrueCrypt**, you need to configure the encrypted system so it doesn't accidentally go into sleep mode. Using the Power Options applet in control panel, set "Put the computer to sleep" to "Never". If the computer has a sleep button, set "When I press the sleep button" to "Do nothing". And be very sure you never choose "Sleep" from the options menu for the shutdown button.

ref (2010) - https://www.pcmag.com/article2/0,2817,2374208,00.asp

## Elcomsoft Forensic Disk Decryptor

> Offers investigators a fast, easy way to access encrypted information stored in crypto containers created by BitLocker, PGP and TrueCrypt

https://www.elcomsoft.com/efdd.html

--

ref (2010) - https://www.wilderssecurity.com/threads/bitlocker-or-truecrypt-can-be-decrypted-in-a-matter-of-minute.288666/

--

## Windows 7 Bitlocker requires TPM

**TPM** stands for “Trusted Platform Module”. It’s a chip on your computer’s motherboard that helps enable tamper-resistant full-disk encryption **without requiring extremely long passphrases**.

[What is a TPM, and Why Does Windows Need One For Disk Encryption?](https://www.howtogeek.com/237232/what-is-a-tpm-and-why-does-windows-need-one-for-disk-encryption/)

[How to Check If Your Computer Has a Trusted Platform Module (TPM) Chip](https://www.howtogeek.com/287737/how-to-check-if-your-computer-has-a-trusted-platform-module-tpm-chip/)

## Windows 10 Bitlocker TPM is not required

You can use BitLocker **without a TPM** chip by using software-based encryption, but it **requires some extra steps for additional authentication**.
[How to use BitLocker Drive Encryption on Windows 10](https://www.windowscentral.com/how-use-bitlocker-encryption-windows-10)

--

My laptop supports TPM (you can see it if is enabled by running **tpm.msc**). But I didnt install the drivers where is 31.83mb

--

How to Access Encrypted Drive using EFDD
https://www.youtube.com/watch?v=K_mI_I8Qdsc

How to open Bitlocker Drive without Password (WinImage converts HDD to VHD)
https://www.youtube.com/watch?v=r-vDYfcR54s

Windows 7 - Bitlocker without TPM
https://www.howtogeek.com/howto/6229/how-to-use-bitlocker-on-drives-without-tpm/

http://www.lostpassword.com/hdd-decryption.htm

https://articles.forensicfocus.com/2016/03/23/bitlocker-whats-new-in-windows-10-november-update-and-how-to-break-it

[Kon-Boot vs. Windows 7 BitLocker (doesnt work)](https://www.mcbsys.com/blog/2009/10/kon-boot-vs-windows-7-bitlocker/)

origin - http://www.pipiscrew.com/?p=11412 bitlocker-or-truecrypt-is-safe