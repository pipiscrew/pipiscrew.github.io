---
title: Nuget Packages are there but missing References
author: PipisCrew
date: 2019-01-07
categories: [.net]
toc: true
---

You need use the NuGet command line in the Package Manager Console:

```js

Update-Package -reinstall

```

src - https://stackoverflow.com/a/42778916

origin - https://www.pipiscrew.com/?p=14580 nuget-packages-are-there-but-missing-references