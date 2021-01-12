---
layout: post
title: Learning vim
published: true
---

## Cursor movement

### Basic movement

* Left, down, up, right

> h,j,k,l

* Start of line (indented)

> _   <-- (underline)

* Start of above line

> \-    <-- (minus)

* Start line of file

> gg

* Last line of file

> G

### Wordwise movement

_Lower case move until meta char | white space_\
_Upper case move until whitespace_

* Start of word (moving forward)

> w\
W

* End of word (moving forward)

> e\
E

* Start of word (moving backward)

> b\
B

* End of word (moving backward)

> ge\
gE

### Sentencewise movement

* Start of line (ignore all indent: unlike '-')

> 0       <-- (number)

* Start of sentence (non-blank)

> ^

* End of sentence

> $

### Pagewise movement

* Move topmost from current page (high)

> H

* Move middle from current page (middle)

> M

* Move lowest from current page (low)

> L

* Start line of Previous page (back)

> ctrl + b

* Start line of Next page (front)

> ctrl + f

* Start line of half-page down

> ctrl + d

* Start line of half-page up

> ctrl + u

### linewise movement

* Move to line

> :[number]

### Blockwise movement

* Move to either pair of block brackets (), {}, [], <>

> %

* Move to {  (moving forward)
  If none, move bottom of page

> ]]

* Move to {  (moving backward)
  If none, move top of page

> [[

* Move to }  (moving forward)
  If none, move bottom of page

> ][

* Move to }  (moving backward)
  If none, move top of page
  
> []

## Edit

### Insertion

* Insert b4 cursor

> i

* Append after cursor

> a

* Insert beginning of line

> I    <-(alphabet upper i)

* Append after end of line

> A

* Append down on next line

> o    <-(alphabet lower o)

* Append up on previous line

> O    <-(alphabet upper o)

### Deletetion

* Delete char at cursor (act like 'del' key)

> x

* Delete char b4 cursor (act like 'backspace' key)

> X

* Delete from cursor to end of line

> D

### Replace

* Delete char and insert

> s

* Delete line and insert ( same as 'cc')

> S

* Delete from cursor to end of line and insert

> C

* Replace char

> r[char]

* Replace until 'esc'

> R

### Multi-line operation

\[operator\]\[count\]\[motion\]

#### operator

* Delete (cut) char / line

> d\
dd

* Yank (copy) char / line

> y\
yy

* Change char / line

> c\
cc

* Make upper / lower / swap case

> gU\
gu\
~

* Increment / Decrement number

> ctrl + a\
ctrl + x

* Indent line right / left

> \>\
\<

* Indent paragraph right / left

> \>}\
\<}

* Repeat previous command

> .

#### motion

```
TODO
```

## File operation

### Basic operation

* Undo

> u

* Redo

> ctrl + r

* Move right tab

> gt

* Move left tab

> gT
