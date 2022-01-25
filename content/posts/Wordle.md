+++
title = "Wordle in One Line"
author = ["Josh Friedlander"]
date = 2022-01-25
draft = false
+++

You may know that the solution for each day's Wordle puzzle is in its source code. Is there a way to grab it from the command line? Naturally.

Start with grabbing the source and outputting to stdin (may as well add `-q`, we don't need the output):

```sh
wget -q -O- powerlanguage.co.uk/wordle/main.e65ce0a5.js
```

Next we just grab the solutions list (look for `Var La`, then note the index of the opening bracket, then go to the matching bracket (using `%` in Vim) and note the closing index):

```sh
cut -c 28467-46985
```

Next, calculate the number of days since the beginning and return this word. This stage took a bit of experimenting, to find today's solution's index, then work backwards to find how many days ago Solution Zero is.

```sh
day=$((($(date "+%s")-$(date -jf "%F" "2021-06-18" "+%s"))/(3600*24)))
```

Then we can use awk to find the word:

```sh
awk -F',' -v day=$day '{print $day}'
```

We now have our answer, but this returns a lot of whitespace, so let's clean it up:

```sh
sed '/^$/d'
```

And remove the quotes, for extra credit:

```sh
tr -d '"'
```

To sum up:

```sh
wget -O- -q powerlanguage.co.uk/wordle/main.e65ce0a5.js | cut -c 28467-46985 | awk -F',' -v day=$((($(date "+%s")-$(date -jf "%F" "2021-06-18" "+%s"))/(3600*24))) '{print $day}' | sed '/^$/d' | tr -d '"'
```

Wordle 220 1/6

🟩🟩🟩🟩🟩
