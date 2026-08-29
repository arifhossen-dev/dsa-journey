# Contains Duplicate

Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.

## Example 1:

```
Input: nums = [1, 2, 3, 3]

Output: true
```

## Example 2:

```
Input: nums = [1, 2, 3, 4]

Output: false
```


# solutions

## The brute-force approach

We are comparing the fast index with the other index till the end. If we get a match, we return true or false. It is an `O(n^2)` complexity. 

### the code example

```python
def hasDuplicate(self, nums: List[int]) -> bool:
    n = len(nums)
    for i in range(n):
        for j in range(i + 1, n):
            if nums[i] == nums[j]:
                return True

    return False

```

On the other hand, we can do it in a more efficient way. 

## The efficient approach

In Python, we have some data structure approach that only allows taking unique values. If it is not unique, it will replace the previous one. If we are able to apply any of those data structures. In this term, we are using a set data structure. We can get easy and less complex solution, Its complexity is `O(n)`. 


### The code example
```python
def hasDuplicate(self, nums: List[int]) -> bool:
    return len(nums) != len(set(nums))
```
