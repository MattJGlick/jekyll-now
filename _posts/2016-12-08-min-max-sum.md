---
layout: post
title: HackerRank - Min Max Sum
---
Hackerrank emailed me this [one](https://www.hackerrank.com/challenges/mini-max-sum) and figured I would give it a go. Given 5 numbers determine the min and max sums of 4 of those numbers. I've expanded my solution to work for n numbers given they are in an array. Trying this one in python as well!

## Realizations:
The min sum of n-1 will always be the total minus the smallest. The max sum will be the total minus the largest. So just traverse the array and then subtract off the mins and the maxes.

## <Solution>
```
numbers = [a, b, c, d, e]

min = numbers[0]
max = numbers[0]
total = 0

for num in numbers:
    if min > num:
        min = num
    if max < num:
        max = num
        
    total += num

print str(total - max) + " " + str(total - min)
```

Defaulted the min and the max to the first number in the array. Traverse through the array and add all the numbers to the sum. Find the min and the max, then finally subtract the min and max from the sums.

### Anaylsis

*Runtime*: O(n)

*Space*: O(1)

Need to traverse through the entire array one time, so O(n) for the space, also only need to store 3 numbers (if I'm excluding the original array) so constant space complexity as well.

