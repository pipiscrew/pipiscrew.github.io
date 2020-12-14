---
title: Visual Studio Code w/ PHP Debug Adapter
author: PipisCrew
date: 2019-11-27
categories: [php]
toc: true
---

https://github.com/felixfbecker/vscode-php-debug

-go to https://xdebug.org/wizard.php and paste the phpinfo(); HTML.

-download the DLL suggesting to **php\ext** directory

-open **php.ini** and paste (add the fullpath to dll)

```js
zend_extension=filepath\php\ext\php_xdebug-2.5.4-7.1-vc14.dll

[XDebug]
xdebug.remote_enable = 1
xdebug.remote_autostart = 1```

-at VSCode install [PHP Debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug)

-if the server running restart it! if not start it!

-open a PHP file, put some breakpoints and **hit F5** (dont use menu Debug > Start Debug)

-Go to the browser and navigate to your browser http://localhost

enable log :

https://github.com/felixfbecker/vscode-php-debug/blob/master/testproject/.vscode/launch.json

* * *

tip1 : you can verify if Xdebugger is running through phpinfo();

tip2 (thanks Nick J Trogh) : by PHP v5.4, you can run a [webserver](http://php.net/manual/en/features.commandline.webserver.php)! using the following :

```jsphp -S localhost:80 -t ../htdocs/```

ref - https://blogs.msdn.microsoft.com/nicktrog/2016/02/11/configuring-visual-studio-code-for-php-development/

* * *

theme - File > preferences > Color theme > Dark+
or
https://marketplace.visualstudio.com/items?itemName=gerane.Theme-Zenburnesque

* * *

## PHP IntelliSense (Completion / Find all References / Go to Definition / Find all symbols / error reporting)

 - https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-intellisense - must update the [language-server](https://github.com/felixfbecker/php-language-server), on a long project (10k files) working, but failed to parse some files. PHP installation required, after installation go to vscode user settings and add the php executable filepath to this property :

```js
//src - https://stackoverflow.com/a/58155087/1320686

//linux
//php installation FEdora v30 - sudo dnf -y install php  php-cli php-fpm php-mysqlnd php-zip php-devel php-gd php-mcrypt php-mbstring php-curl php-xml php-pear php-bcmath php-json
//found the installation path : whereis php
"php.validate.executablePath": "/usr/bin/php",

//windows
"php.validate.executablePath": "C:\\php\\php.exe"
```

where extension folder is :
```js
//linux
$HOME/.vscode/extensions

//windows
%USERPROFILE%\.vscode\extensions
```

[VSCode is unable to watch for file changes in this large workspace](https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc)

VSCode exclude from explorer
```js
//src - https://stackoverflow.com/a/33277809
{
    "files.exclude": {
        "**/.git": true,         // this is a default value
        "**/node_modules": true, // this excludes all folders 
                                 // named "node_modules" from 
                                 // the explore tree
        // alternative version
        "node_modules": true    // this excludes the folder 
                                // only from the root of
                                // your workspace 
    }
}
```

> fix the exceeds size limit of 150000 bytes

![alt](https://i.imgur.com/0kGshkM.jpg)

* * *

## PHP Intelephense - Code intelligence for Visual Studio Code

[homepage](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client)    -   [proof vs PHP IntelliSense](https://medium.com/@Archie22is/how-to-resolve-visual-studio-code-2-php-language-server-parsing-error-on-load-3f160d9fa55d) 

Code style linting - https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs

Format code - https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer

[change the extensions folder location for Visual Studio Code](https://stackoverflow.com/q/40080793/1320686)

34kb ORM - https://medoo.in/

List of PHP editors - https://en.wikipedia.org/wiki/List_of_PHP_editors

* * *

Change brackets border and background color

File > Preferences > Settings > seach for workbench.colorCustomizations, replace with from (v1.14 and above only) :

```js
//https://github.com/Microsoft/vscode/issues/3788#issuecomment-302884093
"workbench.colorCustomizations": {
	"editorBracketMatch.border": "#ff0000",
	"editorBracketMatch.background": "#ff00ff"
}
```

overall :

```js
//https://github.com/Microsoft/vscode/issues/24034#issuecomment-343682162
//https://code.visualstudio.com/docs/getstarted/theme-color-reference#_editor-colors
"workbench.colorCustomizations": {
        "editorBracketMatch.border": "#ff0000",
        "editorBracketMatch.background": "#ff0000",
        "editor.selectionHighlightBackground": "#ff0000",
        "editor.selectionBackground": "#4c5df7d0",
        "editor.selectionForeground": "#ffffff",
        "editor.selectionHighlightBackground": "#7b23e0",

    }
```

![](https://i.imgur.com/GI4CP1O.png)

to disable the auto indent switch to false @ editor.autoIndent

* * *

[Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer) - Extension allows matching brackets to be identified with colours. The user can define which characters to match, and which colours to use.

origin - http://www.pipiscrew.com/?p=11343 visual-studio-code-w-php-debug-adapter