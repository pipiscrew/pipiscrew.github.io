---
title: preg_replace unicode explain - remove emojis
author: PipisCrew
date: 2020-09-05
categories: [php]
toc: true
---

```js
//remove everything except letters, numbers characters (due ^)
preg_replace("/[^A-Za-z0-9]/", '', $str);

//remove everything except letters, numbers characters and dots
preg_replace("/[^A-Za-z0-9.]/", '', $str);

//remove everything except letters, numbers, dots and space (due \s)
preg_replace("/[^A-Za-z0-9\s.]/", '', $str);

//remove everything except letters, numbers, dots, space and #
preg_replace("/[^A-Za-z0-9\s.#]/", '', $str);

//replace abc with def with case insensitive matching (due /i)
preg_replace('/abc/i', 'def', $str);

//replace abc with def with case insensitive matching and acknowledge unicode (due u)
preg_replace('/aγc/iu', 'def', $str);

//for unicode, PHP have properties https://www.php.net/manual/en/regexp.reference.unicode.php
//remove everything except English letters + 
//\p{Greek} Greek letters
//\p{N} numbers
//\p{Zs} space
//when dealing with unicode always use unicode modifier /u
preg_replace("/[^\p{Greek}a-zA-Z\p{N}\p{Zs}]/u", '', $str);
```

Today I would liked to remove the emoticons, which are [thousands](https://emojipedia.org/) and [growing](https://unicode.org/emoji/charts/full-emoji-list.html). There are also [Japanese emoticons](http://kaomoji.ru/en/) and for sure other **shits** exist... The following keeping Greek / English letters, numeric, spaces and normal symbols.

```js
$r = 'asd1|テーブル 테이블◕‿◕ 表 இ௰இ ઊઠઊ ꉨڡꉨ ꈿ۝ꈿ ஞ౩ஞ2|3 |4|5|6| 7|8|9|0|Α|Β|Γ|Δ|Ε|Ζ#|Η|Θ|Ι|Κ|Λ|Μ|Ν|Ξ|Ο|Π|Ρ|Σ|Τ|Υ|Φ|Χ|Ψ|Ω|α|β|γ|δ|ε|ζ|η|θ|ι|κ|λ|μ|ν|ξ|ο|π|ρ|σ|τ|υ|φ|χ|ψ|ω|ς|ά|ί|ό|ώ|ή|ύ|έ|Ά|Ί|Ό|Ώ|Ή|Ύ|ΈΆ|Ί|Ό|Ώ|Ή|Ύ|Έ|A|B|C|D|E|F|G|H|I|J|K|L|M|N|O|P|Q|R|S|T|U|V|W|X|Y|Z|a|b|c|d|e|f|g|h|i|j|k|l|m|n|o|p|q|r|s|t|u|v|w|x|y|z|"||*|/|\|.|,|&|asd~!@#$%&*()_+`-=[\']\;,./<>?:"{}|]';

$time_start = microtime(true);

$symbols = '~!@#$%&*()_+`-=[]\;,./<>?:"{}|\'';
$symbols_esc = preg_quote($symbols , '/');

echo preg_replace("/[^\p{Greek}a-zA-Z\p{N}\p{Zs}$symbols_esc]/u", '', $r);

$time_end = microtime(true);
$execution_time = ($time_end - $time_start) / 60;

echo "  
 $execution_time";
```

origin - https://www.pipiscrew.com/?p=19045 preg_replace-unicode-explain-remove-emojis