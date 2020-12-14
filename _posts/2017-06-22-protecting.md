---
title: Protecting Data with Digital Signatures by Example using MySQL
author: PipisCrew
date: 2017-06-22
categories: [sql]
toc: true
---

```js
/*   Create Jacks private key  */
SET @priv = CREATE_ASYMMETRIC_PRIV_KEY(@algo, @key_len);
select @priv;
INSERT INTO `digsigndemo`.`privuserprivatekey` (`privkkeyuser`,`privatekey`) VALUES  ('signinguser@localhost', @priv);

```

http://mysqlserverteam.com/protecting-data-with-digital-signatures-by-example-using-mysql-enterprise-edition/

You’d first have to be running MySQL Enterprise Edition at version 5.7.9 or greater. That’s a USD5,000/year commitment, so you probably want to download a trial version -- https://www.quora.com/How-do-I-enable-the-CREATE_ASYMMETRIC_PRIV_KEY-function-in-MySQL-5-7

origin - http://www.pipiscrew.com/2017/06/protecting-data-with-digital-signatures-by-example-using-mysql/ protecting-data-with-digital-signatures-by-example-using-mysql