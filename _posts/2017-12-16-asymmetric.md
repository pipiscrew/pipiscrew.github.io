---
title: Asymmetric encryption
author: PipisCrew
date: 2017-12-16
categories: [news]
toc: true
---

> Whitfield Diffie was a key figure in the development of public-key cryptography and digital signatures in the 1970s

https://en.wikipedia.org/wiki/Whitfield_Diffie

Until the 1970s, all publicly known encryption schemes were symmetric: the recipient of an encrypted message would use the same secret key to unscramble the message that the sender had used to scramble it. But that all changed with the invention of asymmetric encryption schemes. These were schemes in which the key to decrypt a message (known as the private key) was different from the key needed to encrypt it (known as the public key)—and there was no practical way for someone who only had the public key to figure out the private key.

This meant you could publish your public key widely, allowing anyone to use it to encrypt a message that only you—as the holder of the private key—could decrypt. This breakthrough transformed the field of cryptography because it became possible for any two people to communicate securely over an unsecured channel without establishing a shared secret first.

Asymmetric encryption also had another groundbreaking application: digital signatures. In normal public-key cryptography, a sender encrypts a message with the recipient's public key and then the recipient decrypts it with her private key. But you can also flip this around: have the sender encrypt a message with his own private key and the recipient decrypt it with the sender's public key.

That doesn't protect the secrecy of the message since anyone can get the public key. Instead, it provides cryptographic proof that the message was created by the owner of the private key. Anyone who has the public key can verify the proof without knowing the private key.

origin - http://www.pipiscrew.com/?p=11650 asymmetric-encryption