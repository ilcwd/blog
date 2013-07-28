---
layout: post
title: "Markdown simple tutorial"
description: ""
category: 
tags: []
---
{% include JB/setup %}



* * *
##Heading

CODE:

	#####I am h5
	### I am h3


SAMPLE:
#####I am h5
###I am h3

***
##Block quotes
CODE:

	>Words
	>>in (nested block)
	>Block quotes

SAMPLE:
>Words
>>in (nested block)
>Block quotes



- -  -
##Code block
a new line + tab.

CODE:

		Here shows the code:

			printf("hello")


SAMPLE:

Here shows the code:

	printf("hello")



- - -
##Lists

###order list

CODE:

	1. item 1
	2. item 2
	5. item 5

SAMPLE:

1. item 1
2. item 2
5. item 5


###unorder list
all `*` `+` `-` are the same.

CODE:
	
	* apple
	* banana
	+ pear
	- pine 

SAMPLE:

* apple
* banana
+ pear
- pine 



- - -
##links

CODE:

	This is an [example](http://example.com "Example") inline link.

	This is a [reference][here] link.

	This is a [implict][] link.

	[here]: http://example.com "Example"
	[implict]: http://example.com "Example"

SAMPLE:

This is an [example](http://example.com "Example") inline link.

This is a [reference][here] link.

This is a [implict][] link.

[here]: http://example.com "Example"
[implict]: http://example.com "Example"


---
##inline emphasis, strong and code

CODE:

	Use `printf()` to *print* your **logs** out.

SAMPLE:

Use `printf()` to *print* your **logs** out.


---
##Images

SYNTAX:

	![Alt text](/path/to/img.jpg "Optional title")
	![Alt text][id]

	[id](/path/to/img.jpg "Optional title")

CODE:
	
	1)
	![Heart Github](https://github.global.ssl.fastly.net/images/modules/contact/heartocat.png "Heart github")
	2)
	![Heart Github][1]

	[1]: https://github.global.ssl.fastly.net/images/modules/contact/heartocat.png "Heart github"

SAMPLE:

1)
![Heart Github](https://github.global.ssl.fastly.net/images/modules/contact/heartocat.png "Heart github")
2)
![Heart Github][1]

[1]: https://github.global.ssl.fastly.net/images/modules/contact/heartocat.png "Heart github"


- - -
##Reference

1. [Markdown 语法说明](http://wowubuntu.com/markdown)