---
title: Android PHP MCrypt
author: PipisCrew
date: 2016-02-11
categories: [php,android]
toc: true
---

reference - [https://github.com/serpro/Android-PHP-Encrypt-Decrypt](https://github.com/serpro/Android-PHP-Encrypt-Decrypt)

usage :
```js
///////////////////////
//JAVA
///////////////////////
MCrypt mcrypt = new MCrypt();

/* Encrypt */

String encrypted = MCrypt.bytesToHex( mcrypt.encrypt("Text to Encrypt") );

/* Decrypt */

String decrypted = new String( mcrypt.decrypt( encrypted ) );

////////////////////////
//PHP
///////////////////////
$mcrypt = new MCrypt();

/* Encrypt */

$encrypted = $mcrypt->encrypt("Text to encrypt");

/* Decrypt */

$decrypted = $mcrypt->decrypt($encrypted);
```

##  PHP MCrypt Class 

```js
//source - https://github.com/serpro/Android-PHP-Encrypt-Decrypt

<?php class="" mcrypt="" {="" private="" $iv='T*TVP^okcafE$nq&' ;="" #same="" as="" in="" java="" private="" $key='^IMKLxglET%TCzAw' ;="" #same="" as="" in="" java="" function="" __construct()="" {="" }="" **="" *="" @param="" string="" $str="" *="" @param="" bool="" $isbinary="" whether="" to="" encrypt="" as="" binary="" or="" not.="" default="" is:="" false="" *="" @return="" string="" encrypted="" data="" */="" function="" encrypt($str,="" $isbinary="false)" {="" $iv="$this-"?>iv;
        $str = $isBinary ? $str : utf8_decode($str);
        $td = mcrypt_module_open('rijndael-128', ' ', 'cbc', $iv);
        mcrypt_generic_init($td, $this->key, $iv);
        $encrypted = mcrypt_generic($td, $str);
        mcrypt_generic_deinit($td);
        mcrypt_module_close($td);
        return $isBinary ? $encrypted : bin2hex($encrypted);
    }
    /**
     * @param string $code
     * @param bool $isBinary whether to decrypt as binary or not. Default is: false
     * @return string Decrypted data
     */
    function decrypt($code, $isBinary = false)
    {
        $code = $isBinary ? $code : $this->hex2bin($code);
        $iv = $this->iv;
        $td = mcrypt_module_open('rijndael-128', ' ', 'cbc', $iv);
        mcrypt_generic_init($td, $this->key, $iv);
        $decrypted = mdecrypt_generic($td, $code);
        mcrypt_generic_deinit($td);
        mcrypt_module_close($td);
        return $isBinary ? trim($decrypted) : utf8_encode(trim($decrypted));
    }
    protected function hex2bin($hexdata)
    {
        $bindata = '';
        for ($i = 0; $i < strlen($hexdata);="" $i="" +="2)" {="" $bindata="" .="chr(hexdec(substr($hexdata," $i,="" 2)));="" }="" return="" $bindata;="" }="" }="" ```=""  =""  ="">

##  Android MCrypt Class 

```js
//source - https://github.com/serpro/Android-PHP-Encrypt-Decrypt
package com.serpro.library.String;

import java.security.NoSuchAlgorithmException;

import javax.crypto.Cipher;
import javax.crypto.NoSuchPaddingException;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;

public class MCrypt {

        static char[] HEX_CHARS = {'0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f'};

        private String iv = "fedcba9876543210";//Dummy iv (CHANGE IT!)
        private IvParameterSpec ivspec;
        private SecretKeySpec keyspec;
        private Cipher cipher;

        private String SecretKey = "0123456789abcdef";//Dummy secretKey (CHANGE IT!)

        public MCrypt()
        {
                ivspec = new IvParameterSpec(iv.getBytes());

                keyspec = new SecretKeySpec(SecretKey.getBytes(), "AES");

                try {
                        cipher = Cipher.getInstance("AES/CBC/NoPadding");
                } catch (NoSuchAlgorithmException e) {
                        // TODO Auto-generated catch block
                        e.printStackTrace();
                } catch (NoSuchPaddingException e) {
                        // TODO Auto-generated catch block
                        e.printStackTrace();
                }
        }

        public byte[] encrypt(String text) throws Exception
        {
                if(text == null || text.length() == 0)
                        throw new Exception("Empty string");

                byte[] encrypted = null;

                try {
                        cipher.init(Cipher.ENCRYPT_MODE, keyspec, ivspec);

                        encrypted = cipher.doFinal(padString(text).getBytes());
                } catch (Exception e)
                {                       
                        throw new Exception("[encrypt] " + e.getMessage());
                }

                return encrypted;
        }

        public byte[] decrypt(String code) throws Exception
        {
                if(code == null || code.length() == 0)
                        throw new Exception("Empty string");

                byte[] decrypted = null;

                try {
                        cipher.init(Cipher.DECRYPT_MODE, keyspec, ivspec);

                        decrypted = cipher.doFinal(hexToBytes(code));
                        //Remove trailing zeroes
                        if( decrypted.length > 0)
                        {
                            int trim = 0;
                            for( int i = decrypted.length - 1; i >= 0; i-- ) if( decrypted[i] == 0 ) trim++;

                            if( trim > 0 )
                            {
                                byte[] newArray = new byte[decrypted.length - trim];
                                System.arraycopy(decrypted, 0, newArray, 0, decrypted.length - trim);
                                decrypted = newArray;
                            }
                        }
                } catch (Exception e)
                {
                        throw new Exception("[decrypt] " + e.getMessage());
                }
                return decrypted;
        }      

        public static String bytesToHex(byte[] buf)
        {
            char[] chars = new char[2 * buf.length];
            for (int i = 0; i < buf.length;="" ++i)="" {="" chars[2="" *="" i]="HEX_CHARS[(buf[i]" &="" 0xf0)="">>> 4];
                chars[2 * i + 1] = HEX_CHARS[buf[i] & 0x0F];
            }
            return new String(chars);
        }

        public static byte[] hexToBytes(String str) {
                if (str==null) {
                        return null;
                } else if (str.length() < 2)="" {="" return="" null;="" }="" else="" {="" int="" len="str.length()" 2;="" byte[]="" buffer="new" byte[len];="" for="" (int="" i="0;"><len; i++)="" {="" buffer[i]="(byte)" integer.parseint(str.substring(i*2,i*2+2),16);="" }="" return="" buffer;="" }="" }="" private="" static="" string="" padstring(string="" source)="" {="" char="" paddingchar="0;" int="" size="16;" int="" x="source.length()" %="" size;="" int="" padlength="size" -="" x;="" for="" (int="" i="0;" i=""></len;>< padlength; i++)
          {
                  source += paddingchar;
          }

          return source;
        }
}
``` padlength;="" i++)="" {="" source="" +="paddingChar;" }="" return="" source;="" }="" }=""></ padlength; i++)
          {
                  source += paddingchar;
          }

          return source;
        }
}
```>

origin - http://www.pipiscrew.com/?p=3737 android-php-mcrypt