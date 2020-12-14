---
title: Regex examples
author: PipisCrew
date: 2020-11-14
categories: [.net]
toc: true
---

### Use Regex.Replace to create a new list of findings

```js
//test input
<td><span align="left">[BMW 2002 FAQ](javascript:onBang('02faq') "www.bmw2002faq.com")</span> <span style="float: right">![02faq](javascript:onBang('02faq') "www.bmw2002faq.com")</span>  </td><td><span align="left">[5channel](javascript:onBang('2channel') "find.5ch.net")</span> <span style="float: right">![2channel](javascript:onBang('2channel') "find.5ch.net")</span>  </td>

string pattern = "<td><span align="\"left\"">[(.*?)](\"(.*?)\" "\"(.*?)\"")</span>(.*?)</td>";
Regex.Replace(txtInput.Text, pattern, "$3 - URL : $1\r\n", RegexOptions.Multiline | RegexOptions.IgnoreCase);

/*
outputs :
BMW 2002 FAQ - URL : www.bmw2002faq.com
5channel - URL : find.5ch.net
*/

//is not doing the job, because (.*) is greedy
<td><span align="\"left\"">[(.*)](\"(.*)\" "\"(.*)\"")</span>(.*)</td>

//use (.*?) instead! is non-greedy
<td><span align="\"left\"">[(.*?)](\"(.*?)\" "\"(.*?)\"")</span>(.*?)</td>

//explained 
https://stackoverflow.com/a/3075150

```

### Use Regex.Replace with MatchEvaluator

```js
//input : ([OrderDatetime] > '5/11/2020 12:00:00 am') AND ([PaymentAmount] = 3) AND ([DeliverDatetime] > '6/12/2020 11:00:00 am') AND ([Status] = 1)
//.          matches any character -- more medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285
//.{50} matches 50 characters -- ^.{5,50}$ a line has between 5-50 chars -- ^.{50,}$ a line has min length 50 chars
string pattern = @"(\d{1,2}/\d{1,2}/\d{4} \d{2}:\d{2}:\d{2})...";
var regex = new Regex(pattern);

string o = regex.Replace(textBox1.Text, delegate(Match match)
{
  DateTime k = DateTime.ParseExact(match.Groups[1].Value, "d/M/yyyy hh:mm:ss", CultureInfo.InvariantCulture);

  return k.ToString("yyyy-MM-dd");
});

//outputs : ([OrderDatetime] > '2020-11-05') AND ([PaymentAmount] = 3) AND ([DeliverDatetime] > '2020-12-06') AND ([Status] = 1)
```

### Validate with Regex.IsMatch

```js
private bool IsCharactersValid(string s)
{
	//Accepts alphanumeric characters in Greek and English, lowercase and uppercase, spaces and the following symbols: /:_().,+-
	return Regex.IsMatch(s, "^[A-ZΑ-Ω0-9 ΆΈΉΗΊΪΌΎΫΥΏ_/:().,+-]+$", RegexOptions.IgnoreCase);
}

private bool IsTelephoneValid(string s)
{
	//Form(..3 - ..15), i.e.(up to 3 characters dash up to 15 characters) example 210-3288000
	return Regex.IsMatch(s, @"^\d{3}-\d{1,15}$");
}

private bool IsMobileValid(string s)
{
	//Form(.+2 - ..15), i.e.(up to 3 characters dash up to 15 characters) example +30-6972222222
	return Regex.IsMatch(s, @"^\+\d{2}-\d{1,15}$");
}

private bool isValidEmail(string s)
{ // src - https://docs.microsoft.com/en-us/dotnet/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format
	return Regex.IsMatch(textBox1.Text, @"^[^@\s]+@[^@\s]+\.[^@\s]+$", RegexOptions.IgnoreCase))
}

```

### OR operator

```js
//input
210-6042612 210-7042612 210-8042612
5210-6042612
+32-5646545645
210-6042612

string pattern = @"(?m)^(\d{3}|\+\d{2})\-\d{1,15}";

Regex reg = new Regex(pattern);
MatchCollection match = reg.Matches(txtInput.Text);

if (match != null)
{
	foreach (Match item in match)
	{
		Console.WriteLine(item.Groups[0].Value);
	}
}

/*
outputs :
210-6042612
+32-5646545645
210-6042612
*/

ref - https://stackoverflow.com/a/14741118
```

**(?m)** = multiline modifier, **^** start of each line
**(\d{3}|\+\d{2})** = 
<div style="padding-left: 30px;">
**\d{3}** = 3 chars numeric 
**|** OR
**\+\d{2}** = the symbol + following 2 chars numeric 
</div>

* * *

### Case insensitive

```js
//src - https://stackoverflow.com/a/2440009
Regex:
    a(?i)bc
Matches:
    a       # match the character 'a'
    (?i)    # enable case insensitive matching
    b       # match the character 'b' or 'B'
    c       # match the character 'c' or 'C'

Regex:
    a(?i)b(?-i)c
Matches:
    a        # match the character 'a'
    (?i)     # enable case insensitive matching
    b        # match the character 'b' or 'B'
    (?-i)    # disable case insensitive matching
    c        # match the character 'c'
```

* * *

MUST READ - [MSDN - Regular Expression Options](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-options)

* * *

```js
^[a-zA-Z]+$
```

Matches any alphabetic string (consisting of the letters a-z, large or small) of size 1 or longer. 
The ^ and $ characters mean "start" and "end" of the line, so they only match full lines consisting of one "word".
Quantifier: + Between one and unlimited times, as many times as possible, giving back as needed [greedy]

src - https://stackoverflow.com/a/34292286

<table "="" border="0"><tbody><tr></tr><tr><td><span>+</span></td><td><span>once or more</span></td></tr><tr><td><span>A+</span></td><td>One or more As, as many as possible (greedy), giving up characters if the engine needs to backtrack (docile)</td></tr><tr><td><span>A+?</span></td><td>One or more As, as few as needed to allow the overall pattern to match (lazy)</td></tr><tr><td><span>A++</span></td><td>One or more As, as many as possible (greedy), not giving up characters if the engine tries to backtrack (possessive)</td></tr><tr><td><span>*</span></td><td><span>zero times or more</span></td></tr><tr><td><span>A*</span></td><td>Zero or more As, as many as possible (greedy), giving up characters if the engine needs to backtrack (docile)</td></tr><tr><td><span>A*?</span></td><td>Zero or more As, as few as needed to allow the overall pattern to match (lazy)</td></tr><tr><td><span>A*+</span></td><td>Zero or more As, as many as possible (greedy), not giving up characters if the engine tries to backtrack (possessive)</td></tr><tr><td><span>?</span></td><td><span>zero times or once</span></td></tr><tr><td><span>A?</span></td><td>Zero or one A, one if possible (greedy), giving up the character if the engine needs to backtrack (docile)</td></tr><tr><td><span>A??</span></td><td>Zero or one A, zero if that still allows the overall pattern to match (lazy)</td></tr><tr><td><span>A?+</span></td><td>Zero or one A, one if possible (greedy), not giving the character if the engine tries to backtrack (possessive)</td></tr><tr><td><span>{x,y}</span></td><td><span>x times at least, y times at most</span></td></tr><tr><td><span>A{2,9}</span></td><td>Two to nine As, as many as possible (greedy), giving up characters if the engine needs to backtrack (docile)</td></tr><tr><td><span>A{2,9}?</span></td><td>Two to nine As, as few as needed to allow the overall pattern to match (lazy)</td></tr><tr><td><span>A{2,9}+</span></td><td>Two to nine As, as many as possible (greedy), not giving up characters if the engine tries to backtrack (possessive)</td></tr><tr><td><span>A{2,}  
A{2,}?  
A{2,}+</span></td><td>Two or more As, greedy and docile as above.  
Two or more As, lazy as above.  
Two or more As, possessive as above.</td></tr><tr><td><span>A{5}</span></td><td>Exactly five As. Fixed repetition: neither greedy nor lazy.</td></tr></tbody></table>

src - [Quantifier Cheat Sheet](http://www.rexegg.com/regex-quantifiers.html#cheat_sheet)

[Regex Storm online tester](http://regexstorm.net/tester) 

[Expresso - regular expression development tool](http://www.ultrapico.com/Expresso.htm)

[Visual Guide to Regular Expression](https://amitness.com/regex/)

#regex

origin - https://www.pipiscrew.com/?p=19189 regex-examples