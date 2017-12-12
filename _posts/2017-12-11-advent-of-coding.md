---
layout: post
title: Advent of Coding 2017
---

One of my friends recently referred me to this terrific programming challenge,
[The Advent of Code](https://adventofcode.com/). Every night at midnight (EST) for 25 nights a new
puzzle comes out. Then tens of thousands of developers rush to be the first one to complete the
challenge. There are no requirements regarding how you solve the problem, but they obviously would
recommend that using a computer is usually optimal.

With that said, sometimes the challenges are actually faster to do by hand. Usually though, some
code is required to complete it quickly. I've been doing most of them as soon as they come out and
I've usually been able to get ranked 300-500 in terms of speed. I'll admit I'd like to see myself get
the top 100 at least once, but as the month goes on the challenges will only get harder and it will
become less likely.

I've also been jumping to the previous years to work on some of the other challenges in my free time.
I'll be posting all of my solutions to each challenge [here](https://github.com/MattJGlick/advent_of_coding).
Usually you'll still be able to run it and get both the Part I and II solutions, but once in awhile
I need to completely overwrite some of the Part I code to get Part II quickly.

For a quick snippet example, here is my solution to Day 6 of 2017, I won't paste the full question.
It can be found on [here](https://adventofcode.com/2017/day/6):

```
import copy

def get_bank_loop(bank):
    seen = []
    rep_count = 0

    while bank not in seen:
        seen.append(copy.deepcopy(bank))
        rep_count += 1

        highest_index = bank.index(max(bank))
        highest_value = bank[highest_index]
        bank[highest_index] = 0

        for _ in range(0, highest_value):
            highest_index = (highest_index + 1) % len(bank)
            bank[highest_index] += 1

    return rep_count, len(seen) - seen.index(bank)


assert get_bank_loop([0, 2, 7, 0]) == (5, 4)
assert get_bank_loop([10, 3, 15, 10, 5, 15, 5, 15, 9, 2, 5, 8, 5, 2, 3, 6]) == (14029, 2765)

with open('input_file.txt') as inputfile:
    print get_bank_loop([int(val) for line in inputfile for val in line.rstrip().split()])
```

If you have any suggestions on how to improve any of my challenges solutions feel free to shoot me
a message!
