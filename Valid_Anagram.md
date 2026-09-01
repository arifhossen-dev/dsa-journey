# Valid Anagram
Given two strings `s` and `t`, return `true` if the two strings are anagrams of each other, otherwise return `false`.

Two strings are **anagrams** if they contain the same characters, with each character appearing the same number of times, regardless of order.


### Example 1:
```python
Input: s = "racecar", t = "carrace"

Output: true
```

### Example 2:
```python
Input: s = "jar", t = "jam"

Output: false
```

### Example 3:
```python
Input: s = "x", t = "x"
Output: true
```
Constraints:

1. `1 <= s.length, t.length <= 5 * 10^4`
2. `s` and `t` consist of lowercase English letters.

---
# Solutions

An **anagram** is a word formed by rearranging the letters of another word, using all the original letters exactly once (for example, `"listen"` and `"silent"`).

## Solution one (The long and more understandable way)

```python
import string

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:

        if(len(s) != len(t)):
            return False

        alphabet_map_s = {letter: 0 for letter in string.ascii_lowercase}
        alphabet_map_t = {letter: 0 for letter in string.ascii_lowercase}


        for item in s:
            alphabet_map_s[item] += 1

        for item in t:
            alphabet_map_t[item] += 1  

        return alphabet_map_s == alphabet_map_t

```

In this solution, We are using Python's built-in string method to create a list of alphabet characters `a` to `z` and  and looping through our string(the `arguments`) and updating the alphabet arrays, then comparing it to each other. It is a more thinkable way to do it, and it is longer.

**The Logic Breakdown**

* **Early Length Check:** `if(len(s) != len(t))` immediately rejects strings of unequal length, saving time.
* **Pre-allocating Hash Maps:** `{letter: 0 for letter in string.ascii_lowercase}` creates two dictionaries (`alphabet_map_s` and `alphabet_map_t`), initializing all 26 letters (`'a'` through `'z'`) with an initial count of `0`.
* **Counting Characters:** The `for` loops iterate over `s` and `t` to increment the counts for the encountered characters.
* **Comparison:** `alphabet_map_s == alphabet_map_t` compares both 26-letter frequency tables. If all counts match, it returns `True`.

**Complexity**

* **Time Complexity:** $O(n)$, where $n$ is the length of the strings. Initializing the 26-letter dictionary takes $O(26)$ ($O(1)$) time, iterating through the strings takes $O(n)$ time, and comparing the dictionaries takes $O(26)$ ($O(1)$) time.
* **Space Complexity:** $O(1)$. Both dictionaries always hold exactly 26 keys regardless of how long the strings are.

## Solution two (The shorter way)
```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:

        if(len(s) != len(t)):
            return False

        return Counter(s) == Counter(t)
```

This solution checks if two words are anagrams by counting their letters and comparing the totals.

**How It Works**

* **`Counter(s)` builds a letter tally:** `Counter` is a built-in Python tool from the `collections` module. It scans a string and counts how many times each character appears, creating a frequency map (like a dictionary).
* `Counter("listen")` becomes `{'l': 1, 'i': 1, 's': 1, 't': 1, 'e': 1, 'n': 1}`
* `Counter("silent")` becomes `{'s': 1, 'i': 1, 'l': 1, 'e': 1, 'n': 1, 't': 1}`


* **`==` compares both tallies:** In Python, comparing two `Counter` objects with `==` checks if they contain the exact same keys with the exact same counts, regardless of the original letter order.
* **`return` gives the result:** If the letter counts match perfectly, it returns `True`. If there is any mismatch in letters or counts (like `"rat"` vs `"car"`), it returns `False`.

**Complexity**

* **Time Complexity:** $O(n)$, where $n$ is the length of the strings. It takes one pass to count characters in each string and one pass to compare the counts.
* **Space Complexity:** $O(1)$ (or $O(k)$ where $k$ is the alphabet size). If the input is standard lowercase English letters, the tally holds at most 26 unique characters.
