---
layout: post
title: HackerRank - Array Left Rotation
---

Back in college I read Cracking the Coding Interview which helped prepare me for interviews and such. Just the other day the author of CTCI put up some problems on HackerRank, so I figured I would give some of them a go!

First problem I worked on was [Array Left Rotation](https://www.hackerrank.com/challenges/ctci-array-left-rotation). You're giving an array of integers and a number to left shift the array on. Then when it's all said and done you need to print all of the elements out.

## Realizations:

This problem is actually really bad. By forcing me to print all of the elements out at the end of the method, I'm not worried about the returning the array. Since I don't need to worry about returning the array, I'm not going to bother swapping the values.

Since I think the problem could be better, I'll do both ways!


## _Proper_ Solution 

All I need to do is traverse through the array starting at the "shift" location, print everything out till the end. Then come back and start at the beginning and print everything out until I get back to the shift.

Since I'm using javascript, and I don't think it's possible to use console.log without a newline, I'm going to be storing the ints in a string

```
function printLeftShift(shift, arr) {
    result = ""
  
    for(i = shift; i < arr.length; i++) {
        result = result.concat(arr[i].toString() + " ")
    }
    
    for(i = 0; i < shift; i++) {
        result = result.concat(arr[i].toString() + " ")
    }

    console.log(result.substring(0, result.length - 1))
}
```

At the very end there I'm removing the extra space that is getting set in the loop. There's a couple ways of handling the stray space, I think this is the cleanest.

### Anaylsis

*Runtime*: O(n)

*Space*: O(n)

The runtime is going to increase linearly with the size of the array, since I need to hit every single index to print out the values. Since I'm slightly restricted by JS as well in terms of the string and printing, I'm also going to be increasing my space complexity linearly.

## Better Solution 

The way cooler way of doing this problem is saying that the purpose is to just return the shifted array and assume that whoever calls it can handle the printing/formatting.

This way I get to take advantage of Javascript's resizeable arrays, which are basically just lists. So I'm going to use "shift" to remove the first index of the array and then "push" to put it on the back of the array. I'll do this for indexes up till the shift value.

```
function printLeftShift(shift, arr) {
    for(i = 0; i < shift; i++) {
        arr.append(arr.shift)) 
    }

    return arr
}
```

### Anaylsis

*Runtime*: O(n)

*Space*: O(1)

This runtime really should O(k), considering it's only based on the shift value. If there is a dataset with 1 million values, and k=1, it's going to be pretty quick. But for the sake of worst case scenario, I'll call this linear run time. Also, I've gotten rid of that nasty string, so I don't use any more data structures, which is way better. So contant space complexity by using the original array.

## Thoughts

Pretty simple problem, I like by "Better Solution" more for sure, but it's worth doing them both I think. Either way good practice for using the array functions.

