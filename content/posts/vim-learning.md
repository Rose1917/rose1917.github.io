+++
title = 'Vim Learning'
date = 2023-12-29T09:22:41+08:00
draft = false
description = 'vim 学习笔记'
+++

# VIM Learning Tutorial

[TOC]



#### 1. VIM AS A LANGUAGE

* Command Pattern：$Verb+Modifer+Noun$

* Verbs: Action performed on the nouns. Here are some examples

  ```shell
  d:delete (delete will not go to insert mode)
  c:change which means delete and into the insert mode
  y:yank
  v:visually select
  ```

* Modifier: Modifiers are used before nouns to describe the way in which you're going to do something

  ```shell
  i:inside(i will not cover the whitespace)
  a:around(a will cover the trailling whitespace,if the object has no trailing whitespace, it will cover the leading whitespace)
  Num: like 1,2,3...
  t:search for something and stops before it
  f:search for something and lands on it
  /:find a string(regex is supported)
  ```

* Nouns: In English, nouns are objects you do something to. With Vim it's the same. Here are some examples:

  ```shell
  w:word
  s:sentence
  ):sentence
  p:paragraph
  }:paragraph
  t:tag
  b:block (in programming)
  character: whatever,eg a,;,*
  ```

**NB: Nouns as motion: specially, you can use single nouns together with a modifier as motion which means moving the cursor to the position you wanted.**

#### 2. Work with your file

* Create a new file or open an existing file: vim filename
* Write to the disk: `:w`
* Exit directly without saving your change:`:q!`
* Write to the disk and exit:`x`
* Save as another file: `saveas file_path`
* Quickly write the disk and exit:`ZZ`
* Execute a command without leaving vim: `:!command`
* Read from another file: append the data of another file to the current file
* Write another file: `n1,n2 w filename`

#### 3. Text Searching

* Basic use: `/string`.or `?string`. The difference between the two pattern is that `/` command will search forward while `?` will search backward. Furthermore, the regular exp is also supported.
* Skip between different hits: use `n` to go to the next instance of result, and use `N` to the previous instance of result.
* Search for the word around cursor: `*`
* Falls on a character: `f<character>`. Similarly, you can use F to search backwards.
* Move till a character:`t<character>`. Similarly, you can use T to search backwards.
* Move to the next instance when you have jumped to a character:`;`
* Move to the previous instance when you have jumped to a character:`,`

#### 4. Moving around in your text

* Basic motions:
  * down: j
  * up: k
  * left: h
  * right: l

* Line motion:
  * beginning of the line: 0(zero by the way)
  * end of line: $
  * move to the first non-blank character in the line: ^
  * move to the specified character on it : f character (mentioned before though)
  * move to the specified character before it: t character

* Word motion:
  * next word: w
  * last word: b
  * move to the end of current word: e
  * next big word: W (ignore delimiters which could break it into two words)
  * last big word: B (ignore delimiters like the example above)

* Sentence or paragraph motion:
  * next sentence: )
  * last sentence: (
  * next paragraph: }
  * last paragraph: {

* Scrolling the screen:
  * Page down: ^ F
  * Page up: ^ B
  * Page half down: ^ D
  * Page half up: ^ U
  * Scroll down one line: ^E
  * Scroll up one line: ^Y
* Moving with the screen
  * Moving to the top of screen: H
  * Moving to the bottom of screen: L
  * Moving to the middle of screen: M
  * Go to the top of file: g g
  * Go to the end of file: G
  * To the specified line: number G

* Moving back and forth
  * Move to the next position: ^ i
  * Move to the previous position: ^ o

#### 5. Mode check

* Three basic modes: Edition mode, visual mode, and command mode. Specially, the visual mode could be regarded as a special command mode. In command mode, you can enter various commands; And in visual mode, you can select text to which generally you perform some commands. And in insert mode, you can change your file.

* The mode check command

  ```sequence
  insert mode->command mode: <esc>
  command mode->insert mode: i/I
  command mode->insert mode: o/O
  command mode->insert mode: a/A
  command mode->visual mode:v/V/ctrl+v
  visual mode->command mode:<esc>
  ```

* Different mode check key:

  * i: insert at the cursor
  * I: insert at the first non-blank position
  * a: insert at the next position
  * A: append at the end of line
  * o: open a new line of next line
  * O: open a new line of the last line
  * <esc>: back to command mode
  * v: to enter the visual mode
  * V: to enter the visual line-wise mode

#### 6. Change motion before Insert mode

* no-action: i
* move the cursor to first character of line: I
* move the cursor to next character: a
* move the cursor to the end of line: A
* new a line: o
* last line: O
* change whatever you defined, like word or sentence or paragraph: c
* replace the current character: r, specially you can use R to replace the current character and enter into insert mode.
* change(Delete) the current line from the cursor to the end of sentence: C
* substitute the current entire line: S

#### 7. Change the case

* Change the case of current selected text: ~

#### 8. Delete the text

* Delete whatever you defined: d modifier nouns

* Delete the whole line: d  d, specially if you want to specify the line number instead of one(by default), you can use d number d.

* Delete the whole line from the cursor: D

* Delete a character: x

* Delete previous character: X

* Join the current line of next line(delete what is between): J

  NB: In vim, by default, you get the cut in your register when you delete something. so you can paste it anywhere after you delete anything.

#### 9. Undo and Redo

* Undo an action: u
* Redo an action: ^ r

#### 10. Repeat

* General introduction： use . to repeat your last command. You can use number + . to specify the number of repeat

#### 11. Copy and Paste

* Copy whatever selected: y
* Copy the current line: y y, also you can specify the yanked lines by use y number y

#### 12. Spell Check

* Start and the cancel: set spell, set no spell
* Move between the word : ]s to the next, [s to the last one.
* See the possible word: z=
* Mark the word as right: z g
* Mark the word as wrong: z w

#### 13. Substitution

* Three arguments while substitution: The match pattern, the target pattern, the scope.
* Find each occurrence **in this line** and substitute it with the target string: :s/text_pattern/target_pattern/g
* The command pattern: find each occurrence **in all lines** and substitute it with the target string: :%s/text_pattern/target_pattern/g
* With prompt and confirm: use c option, like :s/text_pattern/target_pattern/g c
* Only whole word matching: with \<target_pattern\>, like :s/\<t c p\>/target_pattern/g c

* Case sensitive: use i option to set case sensitive

#### 14. Repetition

* Dot command with search: since the dot command will repeat the last serial **commands**(actually it is a serial of keys like shell script), so it is possible to combine the search with . command. Specifically, you can search a pattern and do whatever, the press 'n' to the next instance, use dot command to repeat what you did.
* Macros:  generally speaking, to use MACROS, you only need to do the following three things:
  * Record a command: q+macro_name, press q again to stop the record.
  * Do something: anything
  * Repeat: @+macro_name, you can also use number to specify the repetition times.

#### 15. Text Objects

* Modifiers: modifiers are used to specify the targets(as mentioned above), like i or a which means inside and around respectively.

* Text object: word or paragraph all could be text objects. Additionally, there are some more text objects as shown below

  ```
  w: word
  s: sentence
  p: paragraph
  ': single quote
  ": double quote
  (: parenthesis
  [:brakets
  {:braces
  t:tag
  ```

#### 16. Visual Mode

* To enter the visual mode
  * use v to enter the character-wise visual mode
  * use V to enter the line-wise visual mode
  * use control + v to enter the paragraph mode (which could yank columns)

* Visual select: in the visual mode,you will highlight from the current position of your cursor to the final position. just like you choose the action object, you can also use the same grammar here. for example, you can use `is` to select a sentence, or you can use `a{}` to choose a `{}` block.

* Visual action: after you select what you want, you can do some actions. for instance, copy, delete.
* Combine visual mode with repeat: TO-DO

#### 17. Edit multiple files

* Edit multiple files: you can edit multiple files at the same time, and use `:files` to see all the files, and use `:n` to check the files selected.

* Use multiple windows: to open a new window you just need to type the command  `sp filename`. If the filename is not specified, vim will open the current file. `ctrl+w+j/h` is to used to check the window.
