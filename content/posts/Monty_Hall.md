---
title: Finally Figured Out Monty Hall!
date: 2020-03-30
draft: false
---

Thanks to [this explanation](https://github.com/DeegC/monty_hall_paradox) (coding it out in Ruby made it clearer to me, but it's really the verbal explanation that worked).

At the outset you have doors A, B and C. Given the choice between A or B and C, obviously you would take the latter. That's what you're choosing here! B and C, which combined have a greater chance of being correct. It's more likely that it was in the two you didn't choose: specifically the one of them which isn't wrong. But they still represent 2/3.

As a [HN commenter](https://news.ycombinator.com/item?id=22717754) put it, it's easier to think of it when it's 100 doors. To begin, you choose one. What's the chance you're correct? A measly 1%. You almost certainly got it wrong. Imagine if you could switch to select _the other 99_. Of course you'd do it! Now the host opens the 98 goat doors. The other 99 are 98 goats + 1 `?`. Of course you should switch! _You picked the minority, so the majority of times you are wrong. You're being given a chance to switch to the majority_. Of course, if no door is opened, you're still picking one of 3 - you're still a minority, so it makes no difference if you switch or stay.

