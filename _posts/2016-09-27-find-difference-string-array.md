---
layout: post
title: Leetcode - 389 Find the Difference
---

Next up, finding the spare letter in two different strings. Check out the full problem [here](https://leetcode.com/problems/find-the-difference/). Two different matching strings (s and t), where t has the one extra letter.

## Realizations:

I'm going to be able to treat the strings just like they are arrays: have indexes, can be traversed, etc.

This is going to be pretty easy with a hashmap and two for loops to go through each of the two strings.

The more I'm doing these the more I'm realizing that whenever I see the word "difference" I should immediately think about XOR.

I'm going to assume that the strings are unsorted so I can't do any checking on an index basis.


## Easy Solution - Hash Map 

Going to put each of the elements into a hashmap, making the value the number of occurences. Then after going through the shorter string I'll move on to the longer string and check that value against the values in the second string.

Decreasing the count of that letter in the hashmap. When the count for the letter in t is 0, we know that we've found the extra letter

```
/**
 * @param {string} s
 * @param {string} t
 * @return {character}
 */
var findTheDifference = function(s, t) {
    sObj = {}
    for(i = 0; i < s.length; i++) {
        sObj[s[i]] = (sObj[s[i]] || 0) + 1
    }
    
    for(j = 0; j < t.length; j++) {
        if(sObj[t[j]] > 0) {
            sObj[t[j]]--
        } else {
            return t[j]
        }
    }
};
```

### Anaylsis

*Runtime*: O(n)

*Space*: O(n) 

The runtime is going to be O(2n) to traverse through both strings, it could be a little faster on the second strings considering we could find the difference at the beginning. The space is going to be based purely on the hashmap for s, which is going to linearly increase with the size of s.

## Hard Solution - XOR 

First thing to realize here is that every character has a UTF-16 code unit value (more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt) on that). Meaning that we can really treat these two strings like two different arrys of integers where we're looking for the extra integer

Like I said before, I usually think of XOR when I hear the word "difference". So I'm going to XOR all of the integer representations in both strings and should be left with the integer representation of the extra letter.

```
/**
 * @param {string} s
 * @param {string} t
 * @return {character}
 */
var findTheDifference = function(s, t) {
    value = 0
    for(i = 0; i < s.length; i++) {
        value = value ^ s.charCodeAt(i)
    }
    
    for(j = 0; j < t.length; j++) {
        value = value ^ t.charCodeAt(j)
    }
    
    return String.fromCharCode(value)
};
```

### Anaylsis

*Runtime*: O(n)

*Space*: 1 

We still are traversing through both of the strings, so the runtime is still O(2n), but I was able to remove the need for the extra data structure. I only need to store the remaining value of the integer representation of the letter. So this will be a constant space complexity!

## Thoughts

Overall not too bad, I'm pleased with how quickly I was able to come up with the XOR solution. The hashmap one is pretty simple and would be my first go-to, but I'm pleased that I was able to get a constant space complexity.
