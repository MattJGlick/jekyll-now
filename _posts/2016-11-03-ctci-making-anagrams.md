---
layout: post
title: HackerRank - Strings Making Anagrams 
---
Jump back to HackerRank to do another CTCI problem. Picked the next one on the list and it involes anagrams. Can be found [here](https://www.hackerrank.com/challenges/ctci-making-anagrams).

It reads as follows " Given two strings,  and , that may or may not be of the same length, determine the minimum number of character deletions required to make  and  anagrams. Any characters can be deleted from either of the strings."

Been using Python a lot in the past couple of days, so going to use that.

## Realizations:
Initally I wanted to use a Python set to handle this, then I could just do the differences between them and be done. Unfortunately sets in python don't retain duplicates, so this will fail with duplicates.

There's a couple other ways I could have figured this one out, but I do some research and found something called Counters in Python. I've never used them before, but they seem quite powerful. They're basically just hash maps, but the key is a string and then the value is the count of that key. Seems like exactly what I need for this!

## Python Counter 

```
def number_needed(a, b):
    counterA = Counter(a)
    counterB = Counter(b)

    counterA.subtract(counterB)
    
    total = 0
    for key in counterA:
        total += abs(counterA[key])
    
    return total
```

### Anaylsis

*Runtime*: -- O(n)

*Space*: -- O(n)

The space complexity is fairly easy to calculate here. As we increase the size of the strings, the size of the sets will increase. We will always have 2 sets of the size of their strings, but it will never grow faster than that. As for time complexity, I'm only going to be able to evaluate my for loop (considering I don't fully know the run time of the counter subtraction), which will just be O(n)

## Thoughts

Good problem, got me looking into the Counter, which is definitely something that I'll use in the future.
