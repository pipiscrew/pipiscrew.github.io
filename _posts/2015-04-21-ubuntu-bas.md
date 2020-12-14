---
title: o[ubuntu] bash script
author: PipisCrew
date: 2015-04-21
categories: []
toc: true
---

refence
http://stackoverflow.com/a/3362952/1320686
http://askubuntu.com/a/353282

elementary
```js
#!/bin/bash
# declare STRING variable
STRING="Hello World"
#print variable on a screen
echo $STRING
```

the following script scan all dirs recursive for *.mov filenames and convert them to mp4

```js
#save this script to a file example test.sh
#run via : source test.sh

#!/bin/bash

##when filename contains space(s) is a conflict, resolve it via http://www.cyberciti.biz/tips/handling-filenames-with-spaces-in-bash.html
SAVEIFS=$IFS
IFS=$(echo -en "\n\b")
##when filename contains space(s) is a conflict, resolve it via http://www.cyberciti.biz/tips/handling-filenames-with-spaces-in-bash.html

current_dir=$(cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd)

ddir="/home/admins/Desktop/x/encoded/"
i=100

#create new dir
#mkdir encoded

for g in $current_dir/*;
	do 
$i=i++

#list only *.mov
	for f in $g/*.mov;

		do
k=$i${f##*/}
			#convert to mp4
			ffmpeg -i "$f" -codec:v libx264 -crf 23 -preset medium -codec:a libfdk_aac $ddir/$k;
		done

	done

```

origin - http://www.pipiscrew.com/?p=2908 ubuntu-bash-script