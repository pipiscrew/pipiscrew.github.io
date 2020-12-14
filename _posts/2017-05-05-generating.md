---
title: Generating URL slugs in .NET Core
author: PipisCrew
date: 2017-05-05
categories: [asp.net]
toc: true
---

https://adamhathcock.blog/2017/05/04/generating-url-slugs-in-net-core/

```js
//https://stackoverflow.com/questions/2920744/url-slugify-algorithm-in-c
//https://stackoverflow.com/questions/249087/how-do-i-remove-diacritics-accents-from-a-string-in-net
public static class Slug
{
    public static string GenerateSlug(this string phrase)
    {
        string str = phrase.RemoveDiacritics().ToLower();
        // invalid chars           
        str = Regex.Replace(str, @"[^a-z0-9\s-]", "");
        // convert multiple spaces into one space   
        str = Regex.Replace(str, @"\s+", " ").Trim();
        // cut and trim 
        str = str.Substring(0, str.Length <= 45 ? str.Length : 45).Trim();
        str = Regex.Replace(str, @"\s", "-"); // hyphens   
        return str;
    }

    public static string RemoveDiacritics(this string text)
    {
        var s = new string(text.Normalize(NormalizationForm.FormD)
            .Where(c => CharUnicodeInfo.GetUnicodeCategory(c) != UnicodeCategory.NonSpacingMark)
            .ToArray());

        return s.Normalize(NormalizationForm.FormC);
    }
}
```

origin - http://www.pipiscrew.com/2017/05/generating-url-slugs-in-net-core/ generating-url-slugs-in-net-core