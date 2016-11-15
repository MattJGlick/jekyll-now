---
layout: post
title: HackerRank - Stacks Balanced Brackets 
---
Next one in the CTCI list was a stack question, probably one of the most underrated data structures. The problem can be found [here](https://www.hackerrank.com/challenges/ctci-balanced-brackets). The main gist is that you get a string and need to determine if the string has properly balanced brackets. So for example...

```
{[()]}
{[(])}
{[[(())]]}
```

these would all return:

```
YES
NO
YES
```

## Realizations:
The problem name gives away the obvious data structure. Just need to push the "left" brackets onto the stack as I get them and then pop them off to comapare against the right ones. If we don't find a matching one then we know that we aren't balanced.

## Stack! 
Initially I forgot to account for 2 specific cases. The first was a single right bracket, since it's never added to the stack, the stack was seen as empty. The second one was forgetting to check it the stack had anything on it before popping things off. Both were fairly easy to fix!


```
def is_matched(expression):
    stack = []
    pairs = {
        "[": "]",
        "{": "}",
        "(": ")"
    }   
    
    for char in expression:
        if char in ["[", "(", "{"]:
            stack.append(char)
        elif len(stack) > 0:
            popped = stack.pop()
            
            if pairs[popped] != char:
                return False
        else:
            return False
            
    return len(stack) == 0
```

### Anaylsis

*Runtime*: O(n)

*Space*: O(n)

I need to traverse through the entire string to see if everything matches, so O(n) is the the runtime. Also, the stack will need to store everything and as the size of the string increases so does the stack.

## Thoughts
Fun problem involving a stack, would enjoy doing more of these.

