---
title: Password protect a static HTML page
author: PipisCrew
date: 2017-06-14
categories: [js]
toc: true
---

https://robinmoisson.github.io/staticrypt/
or
https://github.com/robinmoisson/staticrypt/

```js
<!doctype html>

    <style>
        .staticrypt-hr {
            margin-top: 20px;
            margin-bottom: 20px;
            border: 0;
            border-top: 1px solid #eee;
        }

        .staticrypt-page {
            width: 360px;
            padding: 8% 0 0;
            margin: auto;
            box-sizing: border-box;
        }

        .staticrypt-form {
            position: relative;
            z-index: 1;
            background: #FFFFFF;
            max-width: 360px;
            margin: 0 auto 100px;
            padding: 45px;
            text-align: center;
            box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
        }

        .staticrypt-form input {
            outline: 0;
            background: #f2f2f2;
            width: 100%;
            border: 0;
            margin: 0 0 15px;
            padding: 15px;
            box-sizing: border-box;
            font-size: 14px;
        }

        .staticrypt-form .staticrypt-decrypt-button {
            text-transform: uppercase;
            outline: 0;
            background: #4CAF50;
            width: 100%;
            border: 0;
            padding: 15px;
            color: #FFFFFF;
            font-size: 14px;
        }

        .staticrypt-form .staticrypt-decrypt-button:hover, .staticrypt-form .staticrypt-decrypt-button:active, .staticrypt-form .staticrypt-decrypt-button:focus {
            background: #43A047;
        }

        .staticrypt-html {
            height: 100%;
        }

        .staticrypt-body {
            margin-bottom: 1em;
            background: #76b852; /* fallback for old browsers */
            background: -webkit-linear-gradient(right, #76b852, #8DC26F);
            background: -moz-linear-gradient(right, #76b852, #8DC26F);
            background: -o-linear-gradient(right, #76b852, #8DC26F);
            background: linear-gradient(to left, #76b852, #8DC26F);
            font-family: "Arial", sans-serif;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        .staticrypt-instructions {
            margin-top: -1em;
            margin-bottom: 1em;
        }

        .staticrypt-title {
            font-size: 1.5em;
        }

        .staticrypt-footer {
            position: fixed;
            height: 20px;
            font-size: 16px;
            padding: 2px;
            bottom: 0;
            left: 0;
            right: 0;
            margin-bottom: 0;
        }

        .staticrypt-footer p {
            margin: 2px;
            text-align: center;
            float: right;
        }
    </style>

<div class="staticrypt-page">
    <div class="staticrypt-form">
        <div class="staticrypt-instructions">

Protected Page

        </div>

* * *

        <form id="staticrypt-form" action="#" method="post">
            <input id="staticrypt-password" type="password" name="password" placeholder="passphrase">

            <input type="submit" class="staticrypt-decrypt-button" value="DECRYPT">
        </form>
    </div>

</div>
<footer class="staticrypt-footer">

Created with [StatiCrypt](https://robinmoisson.github.io/staticrypt)

</footer>

    $(function () {
        $('#staticrypt-form').submit(function (e) {
            e.preventDefault();

            var passphrase = $('#staticrypt-password').val();
            var encryptedMsg = 'fcabc9486d1502eda51566d1e88493a5b2e822e8799f7e32b5514dfb59003cc5U2FsdGVkX19U3/e+wlbpIlV5mLzY39A1ftqYUGgdE/E=';

            var encryptedHMAC = encryptedMsg.substring(0, 64);
            var encryptedHTML = encryptedMsg.substring(64);

            var decryptedHMAC = CryptoJS.HmacSHA256(encryptedHTML, CryptoJS.SHA256(passphrase)).toString();

            if (decryptedHMAC !== encryptedHMAC) {
                alert('Bad passphrase !');
                return;
            }

            var plainHTML = CryptoJS.AES.decrypt(encryptedHTML, passphrase).toString(CryptoJS.enc.Utf8);

            document.write(plainHTML);
        });
    });

```

origin - http://www.pipiscrew.com/?p=8483 password-protect-a-static-html-page