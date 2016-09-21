---
layout: post
title: Leetcode - 349 Intersection of Two Arrays
---

Hit the random button on Leetcode and ended up with a fairly easy one. I'll put together the obvious solution and see if I can come up with something better afterwards.

Here's the [problem](https://leetcode.com/problems/intersection-of-two-arrays/): "Given two arrays, write a function to compute their intersection. Each element in the result must be unique. The result can be in any order."

## Realizations:

Doesn't look like we can assume that the arrays will be sorted. 

I'm going to try and do it without some of Javascripts array functions (filter, map, etc) These would make thing a lot easier. In reality I'd probably use a 3rd party library like underscore/lodash to handle this considering they have intersections built in.

Will do it by adding a new hashmap and new array. Be interesting to see if I could do it without any new structures (or maybe only 1).

### Hashmap!

I'm going to traverse through the first array adding all of the values to an object. Then traverse through the second array, check to see if it's in the hashmap and add to the resulting array if it is.

```
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    nums1Map = {}
    inter = []
  
    for(i = 0; i < nums1.length; i++) {
        nums1Map[nums1[i]] = 1
    }
  
    for(j = 0; j < nums2.length; j++) {
        if (nums2[j] in nums1Map) {
            inter.push(nums2[j])
            delete nums1Map[nums2[j]]
        }
    }
  
    return inter
};
```

This seems to work fairly well and meet all of the requirements and my ideals. Initially I had the following inside my second for loop:

```
    for(j = 0; j < nums2.length; j++) {
        if (nums2[j] in nums1Map && inter.indexOf(nums2[j])) {
            inter.push(nums2[j])
        }
    }
```

After initially developing this I worried that the indexOf function could be a significant time drain. I would assume that indexOf is doing some sort of array traversal on the backend, which could make my time complexity O(n^2).

I went ahead and refactored to delete the value from the map, that way we never have to deal with even matching on the duplicates, let alone make a decision about them.

### Analysis

*Runtime*: O(n)

*Space*: O(n)

## Thoughts

Overall pretty easy problem. Was about to save myself on runtime by not dealing with a built in array function. Which leads me to think a bit more about making sure I _dont_ use these kind of functions so readily.
