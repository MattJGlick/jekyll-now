---
layout: post
title: Leetcode - 136 Single Number 
---

This is going to be my first attempt at going through a [leetcode problem](https://leetcode.com/problems/single-number/) on my blog. I'm starting out with an easy one to get my feet wet, So lets dive into the problem.

"Given an array of integers, every element appears twice except for one. Find that single one. Note: Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?"  

Javascipt is my language of choice, so I'll be using that throughout.

## Realizations:

I'm going to need to traverse the entire array at least once, ideally only once.

The easy solution is going to be using a hash map, I'll implement that first and then come back and try to do it with no added space.

I think doing it with no added space is going to require me to swap the values within the array or make some kind of analysis on the fly.

## Easy Solution: Hash Map

The basic idea is traverse through the array, add each of the values to a map, if I find the value again, delete it from the map. When it's all done, the last item in the map will be the result

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    map = {}
    
    for(i = 0; i < nums.length; i++) {
        if(map[nums[i]]) {
            delete map[nums[i]]
        } else {
            map[nums[i]] = 1
        }
    }

    return parseInt(Object.keys(map)[0])
};
```

Javascript uses a basic object as a good replacement for a hashmap, so I've named mine `map` here.

The only thing thats slightly complicated and worth noting is:

```
return parseInt(Object.keys(map)[0])
```

This will return all of the keys of the object `map`, The first and only key will be our result. Finally we'll parse it as an int because object keys are set as strings.

### Anaylsis

*Runtime*: O(n)

*Space*: O(n)

While I really didn't increase the space complexity, I did use another data structure to complete it. Lets see if I can do it without the hashmap

## Hard Solution: XOR

My initial assumption with this was I would need to do some rearranging on the array. The more I thought about this the more I realized to do anything meaningful I would need to traverse through the array more than once. Hence increasing my runtime.

So I can't move the values in the array, I can't build a new data structure that will increase with the data. I'll need to set a single int value and do some manipulation on it.

My first instinct was to try and add/subtract the numbers and then I'd be magically left with the result! Obviously considering I won't know which to add or subtract causes a problem here.

Bit manipulation was the only thing left I could think of and had to actually pull up the [wiki](https://en.wikipedia.org/wiki/Bit_manipulation) to remember all of the options. "Toggle a bit" seems to meet our needs here. If we XOR two items that are the same we are left with 0. Hence if we XOR all of the values in the array, all of the same ones will cancel out and we'll be left with our single number. 

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    num = 0
    
    for(i = 0; i < nums.length; i++) {
        num ^= nums[i] 
    }
    
    return num
};
```

### Analysis

*Runtime*: O(n)

*Space*: O(1)

While I still needed to traverse through the full array, I was able to do it without creating any new data structures. Which means constant space complexity, which is an improvement over the hash map.

## Thoughts

While the XOR is definitely the cleaner solution, it definitely wasn't my first thought. I'd be more likely to actually use the hashmap just because it's easy to explain and doesn't save _that_ much extra space. It's fun for a coding problem, but not all that practical.
