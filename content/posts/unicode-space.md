+++
date = '2025-02-16T18:17:24+08:00'
draft = false
title = 'Unicode Space'
tags = ['daily-trick', 'tech']
+++

Some online chat clients, like WhatsApp, WeChat and Identity V, reject empty as well as
space message.

But once you wanna send message like `" "`,
there's a workaround for WeChat: just use Unicode Spaces

That's due to WeChat's `isspace` only checks ASCII space (U+0020) but not others.

One of the most commonly used is U+2000 ("\u2000" in `python`):

{{<copyOnClick "\u2000" "click me to copy">}}

## A full list

|Unicode| 	HTML	|Description 	|Example|
|	-	|	-	|	-	|	-	|
|U+0020 |	&#32    |Space 	|[ ]|
|U+00A0 |	&#160	|No-Break Space 	|[ ]|
|U+2000 |	&#8192 	|En Quad 	|[ ]|
|U+2001 |	&#8193 	|Em Quad 	|[ ]|
|U+2002 |	&#8194 	|En Space 	|[ ]|
|U+2003 |	&#8195 	|Em Space 	|[ ]|
|U+2004 |	&#8196 	|Three-Per-Em Space 	|[ ]|
|U+2005 |	&#8197 	|Four-Per-Em Space 	|[ ]|
|U+2006 |	&#8198 	|Six-Per-Em Space 	|[ ]|
|U+2007 |	&#8199 	|Figure Space 	|[ ]|
|U+2008 |	&#8200 	|Punctuation Space 	|[ ]|
|U+2009 |	&#8201 	|Thin Space 	|[ ]|
|U+200A |	&#8202 	|Hair Space 	|[ ]|
|U+2028 |	&#8232 	|Line Separator 	|[]|
|U+205F |	&#8287 	|Medium Mathematical Space 	|[ ]|
|U+3000 |	&#12288	|Ideographic Space 	|[　]|

ref <https://emptycharacter.com/>

