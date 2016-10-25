---
layout: post
title: HackerRank - Sparse Arrays
---

Picked up [this problem](https://www.hackerrank.com/challenges/sparse-arrays) from HackerRank. Basic overview of the problem is that you get 2 groups of strings, Then you need to evaluate how many times the second set of strings appears in the first group of strings. The input will also supply the length of each array before printing it out.

Sample Input:

```
4
aba
baba
aba
xzxb
3
aba
xzxb
ab
```

Sample Output:

```
2
1
0
```

Explanation: Here, "aba" occurs twice, in the first and third string. The string "xzxb" occurs once in the fourth string, and "ab" does not occur at all.

## Realizations:

Should just be a matter of storing the first set of strings in a map along with the number of occurences of that key. Then afterwards traverse through the second set of strings and see if it occurs in the original map. 

## Hash Map 

```
function processData(input) {
    inputArray = input.split("\n")
    numStrings = parseInt(inputArray[0])
    
    strings = {}
    for(i = 1; i < numStrings + 1; i++) {
        if(strings[inputArray[i]]) {
            strings[inputArray[i]] = strings[inputArray[i]] + 1
        } else {
            strings[inputArray[i]] = 1
        }
    }
    
    queriesStart = numStrings + 2
    for(i = queriesStart; i < inputArray.length; i++) {
        result = strings[inputArray[i]] || 0
        
        console.log(result)
    }
}
```

### Anaylsis

*Runtime*: O(n^2)

*Space*: O(n)

I'm traversing through both set of arrays, so the run time is going to be n^2, Though I'm only storing one set in the hashmap so that will be somewhere < O(n).

## Thoughts

Good review of using maps and key/value pairs. I'm curious if it's possible to do in better than O(n^2) time, but I can't seem to determine exactly how. If it is possible, it would probably need to be around the fact that we already have the first set of strings stored in the array, but I'm not confident in that approach. So I'll be sticking by the O(n^2)/O(n) result.


